## Deploy a static site

This section explains how to create and deploy a static HTML page. It's
worth testing that you can carry out this process before you try to deploy a more complex app.

When you deploy an app, you must select a combination of an organisation and a space (see [Orgs, Spaces and Targets](/#organisations-spaces-amp-targets) for more information). This is called the **target**.

We have provided a ``sandbox`` space in your organisation for you to use for learning about the PaaS. You may want to target the sandbox while you are testing by running:

``cf target -s sandbox``

It's also important to realise that if you deploy an app using the same name and target as an existing app, the original will be replaced. If you are not sure about where to deploy your app, consult the rest of your team.

These steps assume you have already carried out the setup process explained in the [Quick Setup Guide](/#quick-setup-guide) section.

1. In an empty directory, create an `index.html` file.

2. Add some markup to the `index.html` file:


        <html>
          <head>
            <title>Static Site</title>
          </head>
          <body>
            <p>Welcome to the static site!</p>
          </body>
        </html>


3. Create a `manifest.yml` file in the same directory. The manifest file tells
   Cloud Foundry what to do with your app.

        ---
        applications:
        - name: my-static-site
          memory: 64M
          buildpack: staticfile_buildpack

    Replace ``my-static-site`` with a unique name for your app. (You can use ``cf apps`` to see apps which already exist).

    The `memory` line tells the PaaS how much memory to allocate to the app.

    A buildpack provides any framework and runtime support required by an app. If your app was written in Ruby, you would use ``ruby_buildpack``. In this case, we just want to serve a static file, so we use ``staticfile_buildpack``.

4. From the directory where you created the files, run:

    ``
    cf push
    ``

    If you do not specify an app name with the ``push`` command, the name  specified in the manifest file is used.

The site should now be available at `https://APPNAME.cloudapps.digital`. For a production app, you should read the [production checklist](/#production-checklist).
