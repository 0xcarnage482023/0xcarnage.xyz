Setting up a simple blog using sphinx and ablog using a SquareSpace domain, Nginx & DigitalOcean droplet
========================================================================================================

.. post:: 22, November 2023
    :tags: sphinx, ablog, Squarespace, DigitalOcean
    :category: Set-Up
    :author: 0xCarnage

Buying a domain on squarespace and droplet on Digital Ocean:
------------------------------------------------------------

1. Buy a domain on squarespace.

2. Create an Ubuntu droplet on Digital Ocean.

Installing Anaconda and building the website using sphinx and ablog:
--------------------------------------------------------------------

3. Once you create the droplet above, ssh into it as root, create a separate user if you want and install anaconda.

4. Once you install the conda environment, install the following python libraries via pip:

   .. code-block:: python
     
    pip install sphinx ablog pydata_sphinx_theme sphinx_panels

   ..   

    Sphinx: A documentation engine written and used by the Python community.

    ablog: A Sphinx extension that converts any documentation or personal website into a blog.

    pydata_sphinx_theme: A simple, Bootstrap-based Sphinx theme made by the PyData community.

    sphinx_panels: A Sphinx extension for creating panels in a grid layout or as drop-downs.

5. Create a source directory where all the configuration files will be placed.

6. Run the following command in the terminal and answer the follow-ups as shown in the example

   .. code-block:: bash

    $ sphinx-quickstart 
    Welcome to the Sphinx 5.0.2 quickstart utility.
    
    Please enter values for the following settings (just press Enter to
    accept a default value, if one is given in brackets).
    
    Selected root path: .
    
    You have two options for placing the build directory for Sphinx output.
    Either, you use a directory "_build" within the root path, or you separate
    "source" and "build" directories within the root path.
    > Separate source and build directories (y/n) [n]: 
    
    The project name will occur in several places in the built documentation.
    > Project name: Carnage
    > Author name(s): 0xCarnage
    > Project release []: 1.0
    
    If the documents are to be written in a language other than English,
    you can select a language here by its language code. Sphinx will then
    translate text that it generates into that language.
    
    For a list of supported codes, see
    https://www.sphinx-doc.org/en/master/usage/configuration.html#confval-language.
    > Project language [en]: en
    
    Creating file /home/carnage/sphinxblog/conf.py.
    Creating file /home/carnage/sphinxblog/index.rst.
    Creating file /home/carnage/sphinxblog/Makefile.
    Creating file /home/carnage/sphinxblog/make.bat.

   ..   

7. The directory would look something like this:

        *_build/*

        *_static/*
        
        *_templates/*

        *conf.py*
       
        *make.bat*      
     
        *index.rst*
      
        *Makefile* 

8. Open up `conf.py` and update the `extensions` & `html_theme` section as follows:
   
    .. code-block:: python
    
        extensions = [
        "ablog",
        "sphinx.ext.intersphinx",
        "sphinx_panels",
        ]
        
        html_theme = "pydata_sphinx_theme"

    ..

9.  Run `ablog build` to build the static pages. A directory called `_websites` will be created which will contain all the required htm, css and js files. The directory would look something like this at this stage:
    
        *_build/*

        *_static/*
        
        *_templates/*
        
        *_website/*

        *conf.py*
       
        *make.bat*      
     
        *index.rst*
      
        *Makefile* 

Setting up ngnix
----------------

10. Install nginx using the following command:

   .. code-block:: bash
    
      sudo apt install nginx  
 
   ..

11. The default directory for serving webpages is `/var/www/html/`. So we are going to move the entire `_websites` directory we created above to `/var/www/html/`.

12. Open up the nginx conf using the command `sudo nano /etc/nginx/sites-available/default` and add `/var/www/html/_website/` to the `root` section of the file in `server` block. It should look something like this:
    
    .. code-block:: bash
    
        ##
        # You should look at the following URL's in order to grasp a solid understanding
        # of Nginx configuration files in order to fully unleash the power of Nginx.
        # https://www.nginx.com/resources/wiki/start/
        # https://www.nginx.com/resources/wiki/start/topics/tutorials/config_pitfalls/
        # https://wiki.debian.org/Nginx/DirectoryStructure
        #
        # In most cases, administrators will remove this file from sites-enabled/ and
        # leave it as reference inside of sites-available where it will continue to be
        # updated by the nginx packaging team.
        #
        # This file will automatically load configuration files provided by other
        # applications, such as Drupal or Wordpress. These applications will be made
        # available underneath a path with that package name, such as /drupal8.
        #
        # Please see /usr/share/doc/nginx-doc/examples/ for more detailed examples.
        ##
        
        # Default server configuration
        #
        server {
        
            # SSL configuration
            #
            # listen 443 ssl default_server;
            # listen [::]:443 ssl default_server;
            #
            # Note: You should disable gzip for SSL traffic.
            # See: https://bugs.debian.org/773332
            #
            # Read up on ssl_ciphers to ensure a secure configuration.
            # See: https://bugs.debian.org/765782
            #
            # Self signed certs generated by the ssl-cert package
            # Don't use them in a production server!
            #
            # include snippets/snakeoil.conf;
    
            root /var/www/html/_website/;
    
            ...
        }

   ..


13. At this point if you hit up the droplet's IP address on the browser search bar. You'd see a page similar to this:

    .. image:: ../_static/1.png

Now, we'll be looking at how do we connect the domain bought on squarespace with the DO droplet's IP address.

Connecting the Squarespace domain with DO droplet's IP
------------------------------------------------------
TODO

