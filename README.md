# Grunt Sling Content task

This task uses the Sling POST servlet to upload content to a running Sling instance.

Give a root folder to start the mapping from, the task will traverse it recursively and performs the following actions:

-	For each folder, a new node is created of type `nt:unstructured`. If a `.json` file exists with the same name as the directory, this file is read to obtain additional properties for the node representing the folder.
-	For each file which is not a `.json` file, a new node is created of type `nt:file`. If a `.json` file exists with the same name as the directory, this file is read to obtain additional properties for the node representing the file.
-	For each `.json` file, if the file has not been used in one of the following steps, then it is used to create a new node. The properties contained in this file (including `jcr:primaryType`) will be used when the node is created.

The content can be uploaded multiple times. If the resource doesn't exist, the Sling POST servlet will create a new one; otherwise, the existing resource will be updated with new property values and file contents, if they changed after the last upload.

## Options

The task accept the following options:

-	`host`: String, the host name of the Sling instance. Defaults to `localhost`.
-	`port`: integer, the port name of the Sling instance. Defaults to `8080`.
-	`user`:	String, the name of a user which has enough privileges to access the post servlet. Defaults to `admin`.
-	`pass`: String, the password for the user specified in the `user` option. Defaults to `admin`.

## Configuration

This task is a multi-task, so its configuration semantics follow what is already described in the [Grunt documentation](http://gruntjs.com/configuring-tasks). 

The task only accepts input paths which refer to existing folders. Each folder is mapped to the root of the virtual filesystem managed by Sling. In example, if you give as input to the task the folder `root/content` (relative to the root of your project), and this folder contains a file called `page.html`, the path in the Sling repository will be `/page.html`.