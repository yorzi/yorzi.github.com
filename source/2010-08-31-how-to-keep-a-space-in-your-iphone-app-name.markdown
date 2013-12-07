--- 
layout: post
title: How to keep a space in your iPhone App name?
comments: true
categories:
- Filename may not contain whitespace
- iPhone app
- iPhone/iPad
- release
- space in app name
- Titanium
- xcode organizer
status: publish
type: post
published: true
meta: 
  _wp_old_slug: ""
  _edit_last: "1"
---
The answer is, <strong>you can't submit your iPhone App with <em>whitespace</em> in its name</strong>. But you do <strong>be able to add space in your App display name</strong> under icon. I guess your purpose is the second one, you only want to display the space under app icon on device, don't you?

OK, just name your app as whatever name with space before you setup the distribution package, e.g. "Example Name.app". Then,

1) In Xcode Organizer right click on the build date of the app and select "Reveal Archived App in Finder"
2) Open ArchiveInfo.plist in a text editor, edit the attribute "<strong><em><string>Example Name.app</string></em></strong>"
Change that to ExampleName.app and save the file.
4) In Finder remove the space in the file names on both the .app and the .app.dSYM files
5) Once you get back to Xcode Organizer, you should be able to submitting app to itunesconnect successfully.
PS: Also you might want to remove the previously generated .ipa file with the space. just delete the file, a new one will be created after the above steps automatically

Now you are just submitting an app named "ExampleName.app", and its display name will remain "Example Name.app". 
