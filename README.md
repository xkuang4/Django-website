
# Django Website

This README documents the process of developing and deploying my personal website. The project began in October 2022 and was completed in May 2023, with a delay caused by an internal device damage that resulted in the loss of most of the source files. Throughout the development process, two versions of the website were constructed. The first version was successfully deployed on a cloud server, but there were many areas that needed optimization for both viewers and administrators. The second version addressed these issues and was designed with an improved front-end interface. This README also includes information about the website's organization, design, and testing process.


## Authors

- [@Yuk1](https://github.com/xkuang4)


## About Me

I graduated from UW-Madison with majors in Applied Mathematics, Computer Science, and Data Science, and am now an upcoming graduate student in Data Science at Vanderbilt University. Although I am continuing my studies in data science, I have a wide range of interests in other fields as well. One of my passions is developing and deploying websites, which I first learned how to do using Python Flask in a CS course during my junior year at UW-Madison. This website is my first successful deployment, and I designed and developed it entirely on my own.

If you have stumbled upon this document, I hope that the information it contains can be of help to you. Please keep in mind that I am still a beginner in website development, and I welcome any constructive criticism that can help me improve. I am also considering building another website, such as a personal blog or introduction page, in the near future.


## Installation

Python: 3.11

### packages:

```bash
  pip install Django==4.1.6
  pip install Pillow==9.4.0
  pip install django-jazzmin==2.6.0
  pip install django-resized==1.0.2
  pip install gunicorn==20.1.0
  pip install sweetify==2.3.1
  pip install whitenoise==4.0.5
```

### Start Django Project
```bash
  django-damin startproject mysite
```
Before proceeding, please ensure that the terminal panel is in the folder of the project you just created. This can be done by navigating to the project folder using the `cd` command in terminal.

### Create App for Project
```bash
  python manage.py startapp indexPage
```

### Create Admin/superuser
```bash
python manage.py createsuperuser
```


### Run App
```bash
  python manage.py makemigrations
  python manage.py migrate
  python manage.py runserver
```

## HTML Templates
Create a folder called `templates` within the `mysite` directory to store all `HTML` templates that will be rendered by the Django application. 

In `settings.py`. Modify

Templates location
```
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [os.path.join(BASE_DIR, 'templates')],
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]
```

## Static and Media
Create `static` and `media` folder within the `mysite` directory.

In `settings.py`, create and modify the loaction of `static` and `media`

```
STATIC_URL = '/static/'
STATICFILES_DIRS = [os.path.join(BASE_DIR, 'static')]
STATIC_ROOT = os.path.join(BASE_DIR, 'staticfiles')

MEDIA_URL = '/media/'
MEDIA_ROOT = os.path.join(BASE_DIR, 'media')
```
The structure of `static` folder 
```
├─assets
│  ├─css
│  │      404.css
│  │      aboutPage.css
│  │      bootstrap.min.css
│  │      bootstrap.min.css.map
│  │      contactPage.css
│  │      hirePage.css
│  │      indexPage.css
│  │      productPage.css
│  │      samplePage.css
│  │      welcomeAnime.css
│  │      welcomePage.css
│  │
│  └─js
│          bootstrap.min.js
│          bootstrap.min.js.map
│          checkOnPage.js
│          jquery.min.js
│          map.js
│          productFilter.js
│          sweetalert2.all.min.js
│          validate.js
│          welcomeAnime.js
│
└─icons
        404.png
        icon_1.png
        icon_1_resized.png
        icon_2.png
        icon_3.png
        site-icon.png
```
The `assets` is used to store static files such as CSS and JavaScript files, the `icons` folder is used to store icons and other graphics that are used throughout the website, in this case, company logo and favicon.

For each page of my website, I wrote a custom `.css` file to define the appearance and styling of the webpage. Rather than fetching Bootstrap's CSS and JS files from a CDN, I included these files in my website's assets folder to avoid potential accessibility issues due to the Chinese Firewall. 

The structure of `media` folder
```
├─about_us_images
├─additional_images
├─carousel_images
├─common_images
├─images
├─partner_images
└─product_images
    └─product_detail_images
```
These folders are used to store images that can be uploaded by the admin. The path for each folder is defined in the models.py file to specify the category of images and their respective webpage.

## Construct HTML

In my opinion, the functionality of a website should be the top priority and should be built based on the needs and requirements of its intended users. However, the appearance and design of a website also play a crucial role in user experience and can affect the usability and accessibility of the site. In the case of a website used to display products, it may be especially important to prioritize the appearance and design to effectively showcase the products and entice potential customers. 

This web application is built with Bootstrap, a popular front-end web development framework. The website is designed to be responsive and mobile-first, using pre-designed HTML, CSS, and JavaScript templates and components. Bootstrap CSS and JavaScript are the main tools used to develop the user interface and functionality of the website.

In my `templates` folder, I have
```
│  404.html
│
└─main
        about.html
        contact.html
        hire.html
        index.html
        products.html
        sample.html
        welcome.html
```
Note: When using Django's default error handling, the `404.html` template must be placed directly under the `templates` folder. When encountering a 404 error while in production mode (`DEBUG=False`), Django will automatically redirect the user to the custom 404 page specified in the `404.html` template. 

## Project Overview
```
├─.idea
│  └─inspectionProfiles
├─main
│  ├─migrations
│  │  └─__pycache__
│  └─__pycache__
├─media
│  ├─about_us_images
│  ├─additional_images
│  ├─carousel_images
│  ├─common_images
│  ├─images
│  ├─partner_images
│  └─product_images
│      └─product_detail_images
├─mysite
│  └─__pycache__
├─static
│  ├─assets
│  │  ├─css
│  │  └─js
│  ├─fonts
│  │  └─NotoSans
│  └─icons
└─templates
    └─main
```


## Problems

##### 1. The text on the webpage is static, which means that only the website administrator has the ability to change the content by modifying the HTML files directly.
####
##### 2. The order in which uploaded images are displayed on the webpage is determined by the order in which they were uploaded, and cannot be easily changed afterwards.
####
##### 3. The font loading time on the server is currently slow, taking more than 10 seconds to preload the font styles before the webpage is fully loaded.
####
##### 4. In the admin panel, the models are not categorized based on the page they belong to and are presented in an unordered fashion.


## Optimizations

The optimizations made involved a complete rewrite and restructuring of the entire project. These changes were implemented to enhance the performance of the website and improve the user experience for the admin.

### Separate Web App
By command
```bash
 python manage.py startapp xxx
```
I created individual Django apps for each webpage in order to manage them separately
```bash
E:.
├─.idea
│  └─inspectionProfiles
├─aboutpage
│  ├─migrations
│  │  └─__pycache__
│  └─__pycache__
├─contactpage
│  ├─migrations
│  │  └─__pycache__
│  └─__pycache__
├─hirepage
│  ├─migrations
│  │  └─__pycache__
│  └─__pycache__
├─indexpage
│  ├─migrations
│  │  └─__pycache__
│  └─__pycache__
├─media
│  ├─aboutPage
│  │  └─certificate_images
│  ├─icons
│  ├─indexPage
│  │  ├─carousel_images
│  │  └─partner_images
│  ├─productPage
│  │  └─product_images
│  │      └─product_detail_images
│  └─samplePage
│      └─sample_images
├─productpage
│  ├─migrations
│  │  └─__pycache__
│  └─__pycache__
├─samplepage
│  ├─migrations
│  │  └─__pycache__
│  └─__pycache__
├─shunchengsite
│  └─__pycache__
├─static
│  ├─assets
│  │  ├─css
│  │  └─js
│  └─icons
├─templates
│  └─main
├─webelement
│  ├─migrations
│  │  └─__pycache__
│  └─__pycache__
└─welcomepage
    ├─migrations
    │  └─__pycache__
    └─__pycache__
```

#### Note:
The webelement app contains common elements for all webpages, such as the head, header, and footer. However, admin can still customize the font size, background color, head content, and other aspects for each webpage individually.

### Dynamic Content
By adding more fields with default values to models.py, admin now has the ability to change almost all text content displayed on the website, as well as the order of text. This is achieved by modifying the views.py file for each web app.

### Content Display Order
To provide flexibility in the positioning of both text and image content that can be modified by admin, I added an IntegerField to their object. This allows the admin to manually adjust the position of the content displayed on the website by changing their position in ascending order.

### Admin Panel
Web apps are now arranged in the order they appear on the website, and the models are categorized to their corresponding page app. For each page, a custom_style model has been created in models.py for each app, giving the admin more control over customizing the style of the website.


## Deployment

I conducted a search to find a cloud server that meets the requirements for hosting my website, including the necessary configuration and price. After comparing several options, I selected a server that I believe will provide reliable performance and affordability.

Server Config: `Ubuntu 20.04`

Set up necessary packages on server
```bash
  sudo apt update
  sudo apt install python3-pip
  sudo pip3 install virtualenv 
```

After uploading website project to server, I create a virtual environment for my Django project to isolate its dependencies from the global Python installation. 
```bash
  cd /path/to/mysite
  python -m venv env
  source env/bin/activate
  pip install -r requirements.txt
```

`requirements.txt`
```bash
  Django==4.1.6
  Pillow==9.4.0
  django-crispy-forms==2.0
  django-jazzmin==2.6.0
  django-resized==1.0.2
  gunicorn==20.1.0
  sweetify==2.3.1
  whitenoise==4.0.5
```

## Gunicorn Setup

To start and stop the application server in a robust way, I create systemd service and socket files. The Gunicorn socket will listen for connections and automatically start the Gunicorn process to handle them.

```bash
  sudo nano /etc/systemd/system/gunicorn.socket
```
`gunicorn.socket`
```
  [Unit]
  Description=gunicorn socket

  [Socket]
  ListenStream=/run/gunicorn.sock

  [Install]
  WantedBy=sockets.target
```

Then create a systemd service file for Gunicorn.

```bash
  sudo nano /etc/systemd/system/gunicorn.service
```
`gunicorn.service`
```
  [Unit]
  Description=gunicorn daemon
  Requires=gunicorn.socket
  After=network.target

  [Service]
  User= *
  Group=www-data
  WorkingDirectory=/path/to/mysite
  ExecStart=/path/tp/mysite/env/bin/gunicorn \
            --access-logfile - \
            --workers 3 \
            --bind unix:/run/gunicorn.sock \
            mysite.wsgi:application

  [Install]
  WantedBy=multi-user.target
```

Save both files and now start and enable the Gunicorn socket.
```bash
  sudo systemctl start gunicorn.socket
  sudo systemctl enable gunicorn.socket
```

To check the status of gunicorn, run
```bash
  sudo systemctl status gunicorn.socket
```
to make sure it is loaded and active

If any changes are made to `gunicorn.service` or `mysite` project files, run
```bash
  sudo systemctl daemon-reload
  sudo systemctl restart gunicorn
```

## Nginx 
Nginx is a web server that can be used to proxy pass requests to Gunicorn, a Python WSGI HTTP server. This allows Gunicorn to serve a Django web application by receiving requests from Nginx and sending responses back through Nginx to the user's browser.

Install Nginx on server
```bash
  sudo apt install nginx
```

Create and open a new server block in Nginx’s sites-available directory
```bash
  sudo nano /etc/nginx/sites-available/mysite
```
`mysite`
```
server {
    listen 80;
    server_name myDomains;

    location = /favicon.ico { access_log off; log_not_found off; }

    location ^~ /media/ {
        alias /path/to/media/;
    }

    location ^~ /static/ {
        alias /path/to/static/;
    } 

    location / {
        include proxy_params;
        proxy_pass http://unix:/run/gunicorn.sock;
    }
}
```

Save and close the file, then enable the file by linking it to the sites-enabled directory
```
  sudo ln -s /etc/nginx/sites-available/myproject /etc/nginx/sites-enabled
```

To test Nginx configuration status, run
```bash
  sudo nginx -t 
```

If the console outputs without  errors, restart Nginx
```bash
  sudo systemctl restart nginx
```

#### Note: remember to delete `default` file in both `/etc/nginx/sites-available/` and `/etc/nginx/sites-enabled` directory

## SSL Certificates
Download the Let’s Encrypt client: certbot
```bash
  sudo apt-get install certbot
  apt-get install python-certbot-nginx
```

Then run
```bash
   sudo certbot --nginx -d myDomain.com -d www.myDomain.com
```

## Domain
I purchased a domain name on the domain provider Namesilo. In the domain management page, I edited the DNS records to point to my website project hosted on a server and listened by Nginx. It may take some time for the changes to take effect and for the domain to start directing to my website.

## Settings.py
In `settings.py` within `mysite` directory, the default value for `DEBUG` is set to `True`. However, in production, `DEBUG` must set to `False` for security issues.
```
  DEBUG = False
```

Modify allowed host to access this project
```
  ALLOWED_HOSTS = ['myDomain.com', 'www.myDomain.com']
```

Modify other security configuration
```
SECURE_CROSS_ORIGIN_OPENER_POLICY = 'same-origin'
CSRF_COOKIE_SECURE = True
SESSION_COOKIE_SECURE = True
SECURE_SSL_REDIRECT = True
```

## Addition
In my web project `mysite`, I utilized `whitenoise` to serve static files when `DEBUG=False`. Additionally, I implemented the `sweetify` package to enhance the appearance of alert messages during form validation in `contact.html`. Furthermore, to improve the aesthetics of the admin panel, I incorporated `jazzmin` to modify the interface.

## Other Issues
Nginx config has no access of `media` folder in `mysite` directory. Is there any other methods to prevent `403 forbidden error` besides  `chmod 777 /path/to/media`.

TO BE ADDED.
## Feedback

If you have any questions or suggestions, please reach out to me at xkuang4 at wisc dot edu

