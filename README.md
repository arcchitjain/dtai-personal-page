# Simple instructions


## Getting started

For more about how to use Jekyll, check out [this tutorial](https://www.taniarascia.com/make-a-static-website-with-jekyll/).



### Installation

Assuming you have [Ruby](https://www.ruby-lang.org/en/downloads/) and [Bundler](https://bundler.io/) installed on your system, first fork the theme to `github.com:<your-username>/<your-repo-name>` and do the following:

```bash
$ git clone git@github.com:<your-username>/<your-repo-name>.git
$ cd <your-repo-name>
$ bundle install
$ bundle exec jekyll serve
```

### Configuration



1. Launch the site by running this command, which will host the website on [http://localhost:4000/](http://localhost:4000/). Run this command after every ```_config.yml``` update.

```
bundle exec jekyll serve --watch
```

2. Go to ```_config.yml``` and update the properties:
- Your first name in ```first_name```
- Your last name in ```last_name```
- Your personnel number in ```ku_leuven_personnel_number``` to link up your publications (number AFTER the u)
- The courses you teach and have taught under ```teaching```
- Your social media profiles that you would like to link 


3. Go to ```_pages/about.md``` and fill in your own biography to display.

4. Update ```assets/img/prof_pic.jpg``` to a picture of yourself (file name updatable in ```_pages/about.md```)

5. Create your projects by copying and editing the content of the ```_projects folder```

6. If you prefer a different theme color, go to ```_sass/_variables.scss``` and change ```$theme-color: $blue;``` to any color defined above this line.


For more advanced info, see [the original al-folio template](https://github.com/alshedivat/al-folio).




### Deployment

After you are done, **commit** your final changes.
Now, you can deploy your website to [GitHub Pages](https://pages.github.com/) by running the deploy script:

```bash
$ ./bin/deploy [--user]
```
By default, the script uses the `master` branch for the source code and deploys the webpage to `gh-pages`.
The optional flag `--user` tells it to deploy to `master` and use `source` for the source code instead.
Using `master` for deployment is a convention for [user and organization pages](https://help.github.com/articles/user-organization-and-project-pages/).


## License

The theme is available as open source under the terms of the [MIT License](https://opensource.org/licenses/MIT).
