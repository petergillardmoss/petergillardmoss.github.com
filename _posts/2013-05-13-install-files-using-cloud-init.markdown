---
layout: post
title: "Install files using CloudInit"
date: 2013-05-13 12:03
comments: true
categories: 
---

[Cloud-init](https://help.ubuntu.com/community/CloudInit) is one of those killer apps that makes working with Ubuntu a breeze on the cloud (or even other virtualisations such as [lxc](https://help.ubuntu.com/12.04/serverguide/lxc.html)).

Two of the most basic but awesome features of CloudInit is that it supports multi-part data and custom part [handlers](http://foss-boss.blogspot.co.uk/2011/01/advanced-cloud-init-custom-handlers.html).  This allows you to do two things: separate your user data into multiple files and deal with those files in whatever way you please.  So you could upload a shell script and execute it, or upload an sql script to be run against mysql for example.

When setting up a new box you'll undoubtedly have to upload quite a few files (application configuration files etc.) and put them in the right place on the filesystem.  Although the multipart helps you get the files onto the box you end up writing a shell script to copy them to the correct destination.

Well there's an easier way: tarballs.

## 1. Fakeroot
Start by creating a fake root.  You don't need to use [fakeroot](http://man.he.net/man1/fakeroot) to do this but the intent is the same.  Instead replicate the parts of the directory structure you want.  

As an example I want to drop my-app-defaults into /etc/default:

    /home/me/my-app/fake-root/
    |-- etc
    |   |-- default
    |   |   | my-app-defaults

Remember to get your permissions right too.

## 2. Tarball your fake root
This bit's the easy bit.  Simply move to your fake-root and make a tarball:
    (
      cd fake-root
      tar --create --file /home/me/my-app/out/config.tar .
    )

## 3. Add a part handler
Perhaps the best thing about CloudInit is that it's written in Python :).  So it's really simple to write a part handler to extract any tarballs you've uploaded.
    #part-handler
    import os
    import tarfile
    
    def list_types():
      return(['application/x-tar'])
   
    def handle_part(data, ctype, filename, payload):
      target = "/root/%s" % filename
      print("[tarball-file-handler] %s %s" % (ctype, target))
      if ctype == '__begin__' or ctype == '__end__':
         return

      with open(target, 'w') as f:
        f.write(payload)
      tarfile.open(target).extractall('/')

## 4. Add the part handler and tarball to userdata
This is down to you how you do it.  You can follow [these instructions](http://foss-boss.blogspot.co.uk/2011/01/advanced-cloud-init-custom-handlers.html) or you can use something like Ruby's mail:
    mail = Mail.new
    files.each do |file|
      mail.attachments[File.basename(file)] = {
        :encoding => '7bit',
        :content_type => `file --mime --brief #{file}`,
        :content => File.read(file)
      }
    end
    mail.to_s.gsub("\r\n", "\n")

And that's it.  Now cloud-init will do all the hard work for you.  Just give it the tarball and job done!

### Bonus tip:
Gzip your user data.  CloudInit will automatically unzip it on the other side.  This allows you to squeeze more into the [user data's 16kb limit](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AESDG-chapter-instancedata.html) and also keeps things nice and simple as you don't have to worry about compressing that tarball.
