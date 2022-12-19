<h1> Deploy your first Django app in AWS (Beanstalk, Python 3.8 Amazon Linux 2)</h1>

<h2>Choosing a version of Django for production</h2>
<p>When choosing a version of Django for production, it is generally recommended to use the latest stable version of the framework. This ensures that you have access to the latest features and improvements, as well as bug fixes and security updates.</p>
<p>As of December 2022, The long-term support release of Django is <a href="https://docs.djangoproject.com/en/4.1/releases/3.2/">3.2.</a> </p>

<p>Since, we are using an older version of Django in production, it is important to ensure that you are running the latest patch release of the version you are using. Patch releases include bug fixes and security updates, and it is important to keep your Django installation up to date to ensure the security and stability of your application.</p>
<p>Overall, As of December 2022, the best version of django for production is <a href="https://docs.djangoproject.com/en/4.1/releases/3.2.16/">3.2.16</a> </p>

<h3>1. Create a Django project </h3>

<p> 1.1 Use pip to install Django.</p>
<code> pip install django==3.2.16</code>

<p> 1.2 Create a Django project named <code>ebdjango</code>.</p>
<code> django-admin startproject ebdjango .</code>

<p> 1.3 Run your Django site locally with <code>manage.py runserver</code></p>
<code> python manage.py runserver</code>

<h3>2. Create a file named <code>requirements.txt</code>.</h3>

<p>2.1 Use pip to install <code>pipreqs</code></p>
<code> pip install pipreqs</code>

<p>2.2 Use pipreqs to generate a requirements.txt file.</p>
<code> pipreqs .</code>

<h3>3. Configure your Django application for Elastic Beanstalk</h3>
<p>3.1 Create a directory named <code>.ebextensions</code>.</p>
<code> mkdir .ebextensions</code>

<p>3.2 In the .ebextensions directory, add a configuration file named <code>django.config</code> with the following text.</p>
<p><code>
option_settings:<br>
  aws:elasticbeanstalk:container:python:<br>
    WSGIPath: ebdjango.wsgi:application <br>
</code> (In the WSGIPath:, 'ebdjango' is the name of the project and 'wsgi' is the name of the file)</p>

<h3>4. Deploy your site with the EB CLI</h3>

<p>4.1 Install the EB CLI.</p>
<code> pip install awsebcli --upgrade --user</code>

<p> 4.2 Initialize your EB CLI repository with the eb init command.</p>
<code>eb init</code>

<p> 4.3 Create an environment and deploy your application to it with eb create.</p>

<p><code>eb create deploy-eb-al2-env</code> (Creating an environment takes about 5 minutes.)</p>
<p>4.4 When the environment creation process completes, find the domain name of your new environment by running eb status.</p>
<p><code>eb status</code>(Your environment's domain name is the value of the CNAME property.)</p>

<p>4.4.1 Check "Health" section</p>
<p>'Health' status ensure that your applications are running smoothly. If your Elastic Beanstalk environment health is not green, Try to find your mistake.</p>
<p>4.4.2 Once you refactor the files <code> deploy</code> the changes.</p>
<code>eb deploy</code>

<p>Note: repeat 4.4.1 and 4.4.2 till your Elastic Beanstalk environment health is green</p>

<p>4.5 Open the settings.py file in the ebdjango directory. Locate the ALLOWED_HOSTS setting, and then add your application's domain name that you found in the previous step to the setting's value. If you can't find this setting in the file, add it to a new line.</p>
<code>ALLOWED_HOSTS = ['eb-django-app-dev.elasticbeanstalk.com']</code>

<p>4.6 Deploy your changes to your environment.</p>
<code>eb deploy</code>

<p>4.7 When the environment update process completes, open your website with eb open.</p>
<code>eb open </code> <br>
(This opens a browser window using the domain name created for your application. You should see the same Django website that you created and tested locally.)

<h2>Resources</h2>

<p><a href="https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/create-deploy-python-django.html">Deploying a Django application on AWS Elastic Beanstalk</a></p>
<p><a href="https://docs.djangoproject.com/en/4.1/releases/3.2/">Django 3.2 release notes</a></p>
<p><a href="https://docs.djangoproject.com/en/4.1/releases/3.2.16/">Django 3.2.16 release notes</a></p>
<p><a href="https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/eb-cli3-install-windows.html">Install the EB CLI using pip</a></p>
<p><a href="https://github.com/bndr/pipreqs">Generate requirements.txt file for any project based on imports</a></p>
