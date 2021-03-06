BP Attachments
==============

BP Attachments is a "feature as a plugin" component to help other components deal with attachments.
For the "once upon a time": see [ticket 5429](https://buddypress.trac.wordpress.org/ticket/5429)


Required Configurations
----------------------

+ Built in WordPress 3.9, should be ok with 3.8.1
+ Requires at least BuddyPress 2.0-alpha-8020 revision 8160


Installation
------------

+ Before activating the plugin, make sure all the files of the plugin are located in `/wp-content/plugins/bp-attachments`.
+ On multisite configs, make sure to activate BP Attachments at the same level than BuddyPress:
  + if BuddyPress is network activated, activate BP Attachments on the network,
  + if BuddyPress is activated on a specific blog, activate BP Attachments on the same blog.
+ Once activated from the plugins Administration screen, make sure to activate the Attachments component from the BuddyPress settings page (Settings > BuddyPress > Components ).


About the component
-------------------

BP Attachments uses a specific post type `bp_attachment` to organize the files uploaded into a user's profile, or a Group if the BuddyPress Groups component is active.

1. Attachments:
  In the user's profile pages, it adds an "Attachments" subnav where to find all the files a user uploaded. If some attachments are linked to a group, a subnav for Group Attachments will be created.
  In a single Group, if Attachments are enabled in the group settings, it adds an "Attachments" subnav where to find all files attached to the group by all its members.
  Above the subnav in user's profile Attachments page or above the file listing in the Group Attachments page, the "Edit Attachments" button launches the "BP Media Editor" which is a customized version of the WP Media Editor for the `bp_attachment` post type.
  You can use the "BP Media Editor" to add new attachments or manage the ones allready uploaded.
  When on the user's Attachments page, the "BP Media Editor" Manage Attachments tab will list all the files the user uploaded. When on a group's Attachments page, the "BP Media Editor" Manage Attachments tab will list the files the user attached to the current group.

  To edit the groups attached to a file, from his profile attachment page, the user can click on the 'Edit' button of the desired row. Then from the edit page, he will be able to remove his attachment from the selected group or add it to other groups.

  As the goal of this component is to help others deal with attachments, this first version "forces" the Groups component to support Attachments in order to illustrate its features. Other components can support Attachments by defining `$bp->{$component}->can_attachments` to true. In the component settings, BP Attachments will look for the component that support Attachments and will create a new term into the custom taxonomy `bp_component` using the `$bp->{$component}->name` and `$bp->{$component}->slug`.

2. Avatars:
  BP Attachments is managing users and groups avatars. In case of Avatars, the "BP Media Uploader" will only accept single image file upload and once the image uploaded will display it so that the user or the group Admin can crop the avatar.


You can watch a demo of it [here](https://vimeo.com/89982937) ( mute the sound if have difficulties understanding my "franglish" ;) )  


Known bugs
----------

+ BP Media Uploader : the "BackBone" Uploader is using the Attachment model instead of the bpAttachment model, this is the reason why i temporarly disabled an Attachment to be edited from the Attachment Details view just after an upload.


Todos & improvements
--------------------

+ Privacy support: 
  + See boonebgorges's work about BP Docs [wiki](https://github.com/boonebgorges/buddypress-docs/wiki/Attachment-Privacy) & [code](https://github.com/boonebgorges/buddypress-docs/blob/master/includes/attachments.php)
  + Switching from public dir to private dir if the `bp_attachment` status is 'private' into the `BP_Attachments_Upload` Class
  + Moving files from public dir to private and vice and versa in case an Attachment's status was edited by the user
+ Capabilities: need check & improvements
+ Add another way to register a new `bp_component` to allow components generated by a plugin
+ Override the Avatar step of group creation process
+ Build the Administration screens for the Attachments so that an admin can easily moderate user's Attachments
+ Improve the Preview frame using Ajax to load the image so that a private image can be previewed and attachment details and eventual actions can be loaded in an Attachment Details view.
+ Add some styles in the edit attachment user's screen.
+ Check the translation file is loaded
+ ...


Thanks in advance to all of you that will contribute to improve this very first version ;)


