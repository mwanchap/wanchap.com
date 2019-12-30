+++
title = "Getting an .apk into the Google Play store"
date = 2013-12-01T15:04:00Z
updated = 2014-02-19T21:21:56Z
tags = ["Google Play", "Linkdump", "Android Dev"]
blogimport = true 
[author]
	name = "Matt Wanchap"
	uri = "https://www.blogger.com/profile/16465307324394182190"
+++

<br /><div>This is mostly for my own reference but I hope someone else can find it useful too :)</div><ol><li>Disable debugging in your AndroidManifest.xml file by setting android:debuggable="false" in the "application" node.</li><li>cordova build android --release</li><li>jarsigner -verbose -sigalg MD5withRSA -digestalg SHA1 -keystore yourkey.keystore app.apk alias_name (assuming you've generated a key beforehand using keytool in the JDK bin directory)</li><li>zipalign -v 4 app-release-unsigned.apk app.apk (obviously replace "app" with your app name)</li></ol><div>Zipalign must be the last thing that happens!<br />Useful links:<br /><a href="http://developer.android.com/about/dashboards/index.html#Platform">http://developer.android.com/about/dashboards/index.html#Platform</a><br /><a href="http://chris-allen-lane.com/2012/12/phonegap-compiling-a-release-apk-without-using-phonegap-build/">http://chris-allen-lane.com/2012/12/phonegap-compiling-a-release-apk-without-using-phonegap-build/</a><br /><a href="http://iphonedevlog.wordpress.com/2013/08/16/using-phonegap-3-0-cli-on-mac-osx-10-to-build-ios-and-android-projects/">http://iphonedevlog.wordpress.com/2013/08/16/using-phonegap-3-0-cli-on-mac-osx-10-to-build-ios-and-android-projects/</a></div>
