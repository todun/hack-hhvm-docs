The repo for hhvm.com. This contains the website, blog and HHVM/Hack documentation. You'll need PHP v5.3 or greater, and have SQLite installed.

# To update or add documentation

The docs live in `__docs/phpdoc/en`. The `.xml` files and associated directories here are basically the top level outline for the documents. The key ones are `language` and `reference`.

You will update `.xml` files. See `__docs/phpdoc/doc-base/README` for instructions on how to get started. Or just look at the `.xml` files that already exist and copy pasta as much as you need to.


# To validate your additions or changes

To make sure all the XML you have changed or added jives (both in legit XML and in context with the structure of the documentation), you need to run the validator.

The validator is in `__docs/phpdoc/doc-base/configure.php`

To run it:

`php configure.php`

If successful, this will update the `__docs/phpdoc/doc-base/.manual.xml` file that is basically all of the `.xml` files squashed together. This file will be used to render the `.php` files that will actually serve the site.

If unsuccessful, you will see errors. You can run `php configure.php --enable-xml-details` for more detailed XML information.


# To render into PHP files

After validation, it is now time to render the docs to be served. Note that even if you have not made any changes to the documents, you must run the validation step above to generate the `.manual.xml` file.

In `__docs/phd`:

`php render.php -d ../phpdoc/doc-base/.manual.xml -f php -P PHP -o ../../manual/en`

The `.php` files will outputted to the `manual/en` directory.

> To speed up validation, you can try something like:
>   `php render.php -d ../phpdoc/doc-base/.manual.xml -f php -P PHP -o ../../manual/en -t -p language.hack`
> to only render topics that you changed. However, this is not really shippable yet. So before pushing, do a full validation.
> This is good for quick iteration.


# Server up the files locally.

Run a local HHVM server in the root directory, so that `/manual` is a top level path. Navigate to `http://<your local sandbox>/manual/en`.


# Scripts to help.

There are some sample scripts to make this process easier:

`__docs/phpdoc/doc-base/scripts/validate-docs-sample`
`__docs/phd/util/render-docs-sample`

# Other helpful links

https://wiki.php.net/doc/howto/faq
https://wiki.php.net/doc/howto/structure
