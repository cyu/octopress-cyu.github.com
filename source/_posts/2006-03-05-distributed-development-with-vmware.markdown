--- 
wordpress_id: 14
layout: post
title: Distributed Development with VMWare
wordpress_url: http://blog.codeeg.com/2006/03/05/distributed-development-with-vmware/
permalink: /2006/03/05/distributed-development-with-vmware.html
---
If you ever needed to quickly build a distributed environment for development, consider using the free <a href="http://www.vmware.com/download/player/">VMware Player</a>.  This last Friday, I was working at Panera and needed to test some distributed aspects of our application, so I took a shot at using the <a href="http://www.vmware.com/vmtn/appliances/browserapp.html">Browser Appliance VM</a> as my server.  Since the Browser Appliance is just a stripped down Ubuntu installation, you can use the Synaptic Package Manager to install the necessary libraries for development (the <a href="http://www.vmware.com/pdf/bavm_getting_started_100.pdf">Getting Started Guide</a> provided by VMware has instructions on how to use the Synaptic, as well as information on getting root privileges on the VM).

The trickiest part was <a href="https://wiki.ubuntu.com/RestrictedFormats?action=show&amp;redirect=AddingJavaSupport#head-68565ae07a003332e82c9f23706638777396c249">installing Java on Ubuntu</a>, which requires some tricks since Sun's Java for Linux is packaged as an RPM.  Overall, this is a nice setup, since this allows you to create a nice and portable client-server environment.  It also nicely avoids any issues with developers stepping over each other which occurs when working on the same development server.
