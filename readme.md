# MillieText

A platform for free and better textbooks. Built on top of BookStack. Can learn more at https://www.MillieText.com/.

* [Installation Instructions](https://www.bookstackapp.com/docs/admin/installation)
* [Documentation](https://www.bookstackapp.com/docs)
* [Demo Instance](https://demo.bookstackapp.com)
    * [Admin Login](https://demo.bookstackapp.com/login?email=admin@example.com&password=password)

## 📚 Project Definition

MillieText is a place where free textbooks can be accessed. Textbooks that follow our student-friendly format and include promised platform features. Learn more at [MillieText.com](https://discord.gg/ztkBqR2).

This project is built on top of [BookStack](https://github.com/BookStackApp/BookStack). Their project definition is "BookStack is an opinionated wiki system that provides a pleasant and simple out-of-the-box experience. New users to an instance should find the experience intuitive and only basic word-processing skills should be required to get involved in creating content on BookStack. The platform should provide advanced power features to those that desire it but they should not interfere with the core simple user experience."

## 🛣️ Road Map

Below is a feature focused road map view for MillieText to provide a sense of direction of where the project is going. BookStack has a different road map, but as mentioned before, we are taking this project in a different direction to focuse on making textbooks free and better. This road map can change at any point and does not reflect many features and improvements that will also be included as part of the journey along this road map.

- **Hyperlink or Inner Window Feature**
    - *Videos and practice that can be accessed through an "inner window" by clicking §.*
- **Image Block**
    - *Swipe through images in a block where a single image would be in the textbook.*
- **Annotations**
    - *Use basic note tools such as highlighting and underlining through a right-click menu.*
- **Improve WYSIWYG System**
    - *Admin login into a book editor (WYSIWYG system) that allows admins to write new content, publish content, and edit published content.*
- **Flagging and Suggestion**
    - *Flag and suggest edits for words or phrases through a right-click menu.*
- **Analytics**
    - *See data of suggestions and flagged phrases and words.*
- **Flashcards**
    - *Create flashcards in the textbook through a right-click menu.*

## 🚀 Launch

MillieText will launch when two conditions are met:
- `Platform MVP (web app)` - At least 57% of the features are complete (includes main features and tailoring the platform to our needs).
- `Textbook MVP` - At least half of a single textbook with a cited textbook, complete student-friendly design, and videos attached to each §.

## 🛠️ Development & Testing

All development on MillieText is currently done on the master branch. When it's time for a release the master branch is merged into release with built & minified CSS & JS then tagged at its version. Here are the current development requirements:

* [Node.js](https://nodejs.org/en/) v14.0+

This project uses SASS for CSS development and this is built, along with the JavaScript, using a range of npm scripts. The below npm commands can be used to install the dependencies & run the build tasks:

``` bash
# Install NPM Dependencies
npm install

# Build assets for development
npm run build

# Build and minify assets for production
npm run production

# Build for dev (With sourcemaps) and watch for changes
npm run dev
```

BookStack has many integration tests that use Laravel's built-in testing capabilities which makes use of PHPUnit. MillieText will be doing the same. There is a `mysql_testing` database defined within the app config which is what is used by PHPUnit. This database is set with the database name, user name and password all defined as `bookstack-test`. You will have to create that database and that set of credentials before testing.

The testing database will also need migrating and seeding beforehand. This can be done with the following commands:

``` bash
php artisan migrate --database=mysql_testing
php artisan db:seed --class=DummyContentSeeder --database=mysql_testing
```

Once done you can run `php vendor/bin/phpunit` in the application root directory to run all tests.

### 📜 Code Standards

PHP code style is enforced automatically [using StyleCI](https://github.styleci.io/repos/41589337). 
If submitting a PR, any formatting changes to be made will be automatically fixed after merging.  

### 🐋 Development using Docker

This repository ships with a Docker Compose configuration intended for development purposes. It'll build a PHP image with all needed extensions installed and start up a MySQL server and a Node image watching the UI assets.

To get started, make sure you meet the following requirements:

- Docker and Docker Compose are installed
- Your user is part of the `docker` group

If all the conditions are met, you can proceed with the following steps:

1. **Copy `.env.example` to `.env`**, change `APP_KEY` to a random 32 char string and set `APP_ENV` to `local`.
2. Make sure **port 8080 is unused** *or else* change `DEV_PORT` to a free port on your host.
3. **Run `chgrp -R docker storage`**. The development container will chown the `storage` directory to the `www-data` user inside the container so BookStack can write to it. You need to change the group to your host's `docker` group here to not lose access to the `storage` directory.
4. **Run `docker-compose up`** and wait until the image is built and all database migrations have been done.
5. You can now login with `admin@admin.com` and `password` as password on `localhost:8080` (or another port if specified).

If needed, You'll be able to run any artisan commands via docker-compose like so:

```bash
docker-compose run app php artisan list
```

The docker-compose setup runs an instance of [MailHog](https://github.com/mailhog/MailHog) and sets environment variables to redirect any BookStack-sent emails to MailHog. You can view this mail via the MailHog web interface on `localhost:8025`. You can change the port MailHog is accessible on by setting a `DEV_MAIL_PORT` environment variable.

#### Running tests

After starting the general development Docker, migrate & seed the testing database:

 ```bash
# This only needs to be done once
docker-compose run app php artisan migrate --database=mysql_testing
docker-compose run app php artisan db:seed --class=DummyContentSeeder --database=mysql_testing
```

Once the database has been migrated & seeded, you can run the tests like so:

 ```bash
docker-compose run app php vendor/bin/phpunit
```

## 🌎 Translations (from BookStack)

Translations for text within BookStack is managed through the [BookStack project on Crowdin](https://crowdin.com/project/bookstack). Some strings have colon-prefixed variables in such as `:userName`. Leave these values as they are as they will be replaced at run-time. Crowdin is the preferred way to provide translations, otherwise the raw translations files can be found within the `resources/lang` path.

Please note, translations in BookStack are provided to the "Crowdin Global Translation Memory" which helps BookStack and other projects with finding translations. If you are not happy with contributing to this then providing translations to BookStack, even manually via GitHub, is not advised.

Abide by this as MillieText will be integrating this feature as BookStack works on it. 

## 🎁 Contributing, Issues & Pull Requests

Feel free to create issues to request new features or to report bugs & problems. Just please follow the template given when creating the issue.

Pull requests should be created from the `master` branch since they will be merged back into `master` once done. Please do not build from or request a merge into the `release` branch as this is only for publishing releases. If you are looking to alter CSS or JavaScript content please edit the source files found in `resources/`. Any CSS or JS files within `public` are built from these source files and therefore should not be edited directly.

The project's code of conduct [can be found here](https://github.com/MillieText/webapp/blob/master/.github/CODE_OF_CONDUCT.md).

## 🔒 Security (from BookStack)

Security information for administering a BookStack instance can be found on the [documentation site here](https://www.bookstackapp.com/docs/admin/security/).

If you'd like to be notified of new potential security concerns you can [sign-up to the BookStack security mailing list](https://updates.bookstackapp.com/signup/bookstack-security-updates).

If you would like to report a security concern, details of doing so can [can be found here](https://github.com/BookStackApp/BookStack/blob/master/.github/SECURITY.md).

## ♿ Accessibility (from BookStack)

We want BookStack to remain accessible to as many people as possible. We aim for at least WCAG 2.1 Level A standards where possible although we do not strictly test this upon each release. If you come across any accessibility issues please feel free to open an issue.

## 🖥️ Website, Docs & Blog

The website which contains the project docs & Blog can be found in the [MillieText/landing](https://github.com/MillieText/landing) repo.

## ⚖️ License

The BookStack source is provided under the MIT License. The libraries used by, and included with, MillieText are provided under their own licenses.

## 👪 Attribution

The great people that have worked to build and improve BookStack can [be seen here](https://github.com/MillieText/webapp/graphs/contributors).

These are the great open-source projects used to help build MillieText:

* [BookStack](https://www.bookstackapp.com/)
* [Laravel](http://laravel.com/)
* [TinyMCE](https://www.tinymce.com/)
* [CodeMirror](https://codemirror.net)
* [Sortable](https://github.com/SortableJS/Sortable)
* [Google Material Icons](https://material.io/icons/)
* [Dropzone.js](http://www.dropzonejs.com/)
* [clipboard.js](https://clipboardjs.com/)
* [markdown-it](https://github.com/markdown-it/markdown-it) and [markdown-it-task-lists](https://github.com/revin/markdown-it-task-lists)
* [BarryVD/Dompdf](https://github.com/barryvdh/laravel-dompdf)
* [BarryVD/Snappy (WKHTML2PDF)](https://github.com/barryvdh/laravel-snappy)
* [WKHTMLtoPDF](http://wkhtmltopdf.org/index.html)
* [diagrams.net](https://github.com/jgraph/drawio)
* [OneLogin's SAML PHP Toolkit](https://github.com/onelogin/php-saml)
* [League/CommonMark](https://commonmark.thephpleague.com/)
* [League/Flysystem](https://flysystem.thephpleague.com)
* [StyleCI](https://styleci.io/)
* [pragmarx/google2fa](https://github.com/antonioribeiro/google2fa)
* [Bacon/BaconQrCode](https://github.com/Bacon/BaconQrCode)
* [phpseclib](https://github.com/phpseclib/phpseclib)
* [Clockwork](https://github.com/itsgoingd/clockwork)
* [PHPStan](https://phpstan.org/) & [Larastan](https://github.com/nunomaduro/larastan)
