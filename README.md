# custom-node-openshift
Install a custom version of NodeJS on openshift, this is a fork of: https://github.com/ramr/nodejs-custom-version-openshift

## How to install
Create an account at http://openshift.redhat.com/

Create a namespace, if you haven't already do so

    rhc domain create <yournamespace>

Create a nodejs application (you can name it anything via -a)

    rhc app create -a custom  -t nodejs-0.10

Add this `github custom-node-openshift` repository

    cd palinode
    git remote add custom -m master git://github.com/miguelcostero/custom-node-openshift.git
    git pull -s recursive -X theirs custom master

Optionally, specify the custom version of Node.js you want to run with
(Default is v4.2.3).
If you want to more later version of Node (example v4.2.42), you can change
to that by just writing it to the end of the NODEJS_VERSION file and
committing that change.

    echo 4.2.42 >> .openshift/markers/NODEJS_VERSION
    #
    # Or alternatively, edit the .openshift/markers/NODEJS_VERSION file
    # in your favorite editor aka vi ;^)
    #
    # Note: 4.2.42 doesn't exist (as yet) and is a fictitious version
    #       mentioned here solely for demonstrative purposes.
    #
    git commit . -m 'now using Node version 4.2.42'

Then push the repo to OpenShift

    git push

That's it, you can now checkout your application at:

    http://custom-$yournamespace.rhcloud.com
    ( See env @ http://custom-$yournamespace.rhcloud.com/env )
