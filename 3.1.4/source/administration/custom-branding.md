# Custom branding

Credential Manager allows administrators to alter the application's appearance to match their organization's look and feel. Intermediate-level knowledge of CSS is required for this task.

## Getting Default Theme Files

The design is driven by a few images and CSS stylesheets. These are inside the app's war file, so let's extract those to a separate location:

* `cd` to the app's war file directory. For instance `/opt/gluu/jetty/cred-manager/webapps`

* Make the Java bin directory available in your PATH. For example:

```
	JAVA_HOME=/opt/gluu-server-3.1.4/opt/jdk1.8.0_162
	export JAVA_HOME
	PATH=$PATH:$JAVA_HOME/bin
```

* Run the following:

```
	$ jar -xf cred-manager.war images
	$ jar -xf cred-manager.war styles
``` 

* Now you should see two new directories. Move those to `/opt/gluu/jetty/cred-manager/static`. The following is an example to move `images` and `styles`:

```
	$ mv images /opt/gluu/jetty/cred-manager/static/images
	$ mv styles /opt/gluu/jetty/cred-manager/static/styles
```

* Ensure the operating system user that runs Jetty has read permissions on the files added. You may do the following to solve it:

```
$ chown -R jetty:jetty /opt/gluu/jetty/cred-manager/static/
```

Glance at the contents of both directories (`images` and `styles`). If you think that editing those CSS files and replacing some images will customize the look and feel, you are on the line.

Look through the `images` and `styles` directories to see the current contents. By editing those CSS files and replacing some images, the Credential Manager's look and feel can be customized.

## Enable Customizations

For Credential Manager to read images and styles from the custom directory, you need to supply its location:

* With your admin credentials, log into the app. In the admin dashboard, click on "Branding" and choose "Use external assets directory".

* Do a subtle edition of a file to test if things are going well. For instance, open the file `styles/common.css`, locate the CSS selector for *header* and change the background color to red, like this:

```
	.header{
		...
		background: red;
		...
	}
```

* Save `common.css`

* Open a private browsing session. Log in, and you will see a beautiful red header!. Private browsing is convenient for testing, otherwise, you'd have to clear your recent browser history constantly after every change.

!!! Note: 
    The URL `https://<host-name>/cred-manager/custom` maps to the directory where you have placed the `images` and `styles` folder.
    
## Applying your Customizations

Here are some tips to take into account to match your company design:

* This app uses separate stylesheets for desktop and mobile environments (`desktop.css` and `mobile.css`, respectively). File `common.css` stores styles that apply for both environments.

* File names for images must remain unchanged, thus, to use an image of your own, you need to replace the current version of the file. This holds for company logo, icons, etc.

* Inspect the DOM tree generated for application pages and determine the CSS selectors you need to edit or the kind of things your have to add in order to alter the appearance. Use your web browser's facilities to inspect web page composition: this is usually part of any browser's developer toolbar. Moreover, they allow you to change styles on the fly so you can play a lot before applying the real changes.

* Once you edit, add, or delete images, there is no need to restart the application to see the changes. However, most static files are cached by browsers, so you will need to clear the browser history for the current day. The `shift+Ctrl+supr` combination does the job in most browsers. Leave the cookies option unchecked, so there is no need to log in after every refresh.

* Ignore the `jquery-ui-1.12.1.min` file. You may even erase the file.

* If you are modifying files/images and not seeing the changes, try hitting the resource URL directly in a new browser tab. For example, to load the `common.css` file in your browser, you should visit `https://<host-name>/cred-manager/custom/styles/common.css`. That way, you can determine if your changes are there; if they are not, refresh with **`F5`**. If you still get the same content, you are not deleting your cache properly. Close all tabs, empty the recent cache and try again.

## Reverting to Default Theme

If for any reason you wish to restore the default theme, select "Use default (Gluu Inc.) theme" in the admin dashboard.

## Some Examples

Here are solutions for common use cases:

### Use a different logo

* Replace the file at `custom/images/logo.png` with your own PNG file.

* Edit the *logo* CSS selector in the `desktop.css` and `mobile.css` files. Assign the real dimensions to use for the image when displayed in desktop and mobile browsers. Dimensions should be in line with the actual width/height ratio of the original image.

### Use a Different Favicon

This the easiest customization. Just replace `custom/images/favicon.ico`.

### Change the Font Used in Text

The vast majority of text that appears in the application uses the same font. To alter the default font, edit the *z-label* CSS selector in the `desktop.css` and `mobile.css` files. Change the value for *font-family* (you may also alter *font-size*). For example:

```
	.z-label{
	...
		font-family: courier;
	...
	}
```

### Change Button Colors

Say you'd prefer the buttons to be blue, add the following rules to `common.css` (you may append them at the end of the file):

```
	.btn-success, .btn-success:hover, .btn-success:focus, .btn-success:active,
	.btn-success.active, .btn-success.disabled {
		background-color: #00F;
		border-color: #00F;
	}
```

### Adjust Width of App's Content Area for Desktop

Edit `desktop.css` file and change *mainDiv* by setting a different value for *width*:

```
	.mainDiv{
		...
			width:600px;
		...
	}
```

Now Credential Manager should neatly accomodate the updated width.
