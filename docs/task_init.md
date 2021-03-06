[Grunt homepage](https://github.com/cowboy/grunt) | [Documentation table of contents](toc.md)

# init (built-in task)
Generate project scaffolding from a predefined template.

## About <a name="about" href="#about" title="Link to this section">⚑</a>

The `init` task initializes a new project, based on the current environment and the answers to a few questions. Once complete, a [grunt.js configuration file](getting_started.md) will be generated along with a complete directory structure, including a basic readme, license, package.json, sample source files and unit tests (etc).

The exact files and contents created depend on the template chosen along with the answers to the questions asked.

Unlike other tasks, init should only ever be run once for a project. Typically, it is run at the very beginning before work has begun, but it can be run later. **Just keep in mind that new files are generated, so for existing projects, ensure that everything is already committed first.**

## Usage examples <a name="usage-examples" href="#usage-examples" title="Link to this section">⚑</a>

Change to a new directory, and type in `grunt init:TEMPLATE` where TEMPLATE is one of the following templates. Answer the questions. Watch grunt do its thing. Done. Now you have fully initialized project scaffolding that you can customize, `grunt` and publish.

## Built-in templates <a name="built-in-templates" href="#built-in-templates" title="Link to this section">⚑</a>

The init task currently supports a number of built-in templates.

### gruntfile <a name="gruntfile" href="#gruntfile" title="Link to this section">⚑</a>
Generated via `grunt init:gruntfile`, this customizable template creates a single [grunt.js gruntfile](getting_started.md) based on the answers to a few questions and some highly advanced "fuzzy logic" that tries to determine source and unit test paths. This is the template you want to use to generate a gruntfile for an existing project.

If your code is DOM-related, [QUnit unit tests](task_qunit.md) will be used, otherwise Nodeunit unit tests will be used. Where appropriate, predefined [lint](task_lint.md), [concat](task_concat.md) and [minification](task_min.md) tasks are generated. Also, depending on the library used, JSHint globals may be predefined (just `jQuery` for now).

**You will most likely need to edit the generated grunt.js file before running `grunt`. If you run grunt after generating grunt.js, and it exits with errors, edit the grunt.js file!**

_See an [example repo](https://github.com/cowboy/grunt-gruntfile-example/tree/HEAD~1) generated by this template along with the [creation transcript](https://github.com/cowboy/grunt-gruntfile-example/blob/master/README.md)._

### commonjs <a name="commonjs" href="#commonjs" title="Link to this section">⚑</a>
Generated via `grunt init:commonjs`, this customizable template creates an entire project directory structure with a [grunt.js gruntfile](getting_started.md), Npm-friendly package.json file, sample [CommonJS](http://www.commonjs.org/) source file and Nodeunit unit tests.

In addition, predefined [lint](task_lint.md), [concat](task_concat.md) and [minification](task_min.md) tasks are generated.

_See an [example repo](https://github.com/cowboy/grunt-commonjs-example/tree/HEAD~1) generated by this template along with the [creation transcript](https://github.com/cowboy/grunt-commonjs-example/blob/master/README.md)._

### jquery <a name="jquery" href="#jquery" title="Link to this section">⚑</a>
Generated via `grunt init:jquery`, this customizable template creates an entire project directory structure with a [grunt.js gruntfile](getting_started.md), [jQuery package.json](https://github.com/jquery/plugins.jquery.com/blob/master/docs/package.md) file, [jQuery](http://jquery.com/) plugin file and [QUnit unit tests](task_qunit.md).

In addition, predefined [lint](task_lint.md), [concat](task_concat.md) and [minification](task_min.md) tasks are generated.

_See an [example repo](https://github.com/cowboy/grunt-jquery-example/tree/HEAD~1) generated by this template along with the [creation transcript](https://github.com/cowboy/grunt-jquery-example/blob/master/README.md)._

### node <a name="node" href="#node" title="Link to this section">⚑</a>
Generated via `grunt init:node`, this customizable template creates an entire project directory structure with a [grunt.js gruntfile](getting_started.md), Npm package.json file, sample [Node.js](http://nodejs.org/) source file and Nodeunit unit tests.

_See an [example repo](https://github.com/cowboy/grunt-node-example/tree/HEAD~1) generated by this template along with the [creation transcript](https://github.com/cowboy/grunt-node-example/blob/master/README.md)._

## Specifying default prompt answers <a name="specifying-default-prompt-answers" href="#specifying-default-prompt-answers" title="Link to this section">⚑</a>
Each init prompt either has a default value hard-coded or it looks at the current enviroment to attempt to determine that default value. If you want to override a particular prompt's default value, you can do so in the optional OS X or Linux `~/.grunt/tasks/init/defaults.json` or Windows `%USERPROFILE%\.grunt\tasks\init\defaults.json` file.

For example, my `defaults.json` file looks like this, because I want to use a slightly different name than the default name, I want to exclude my email address, and I want to specify an author url automatically.

```javascript
{
  "author_name": "\"Cowboy\" Ben Alman",
  "author_email": "none",
  "author_url": "http://benalman.com/"
}
```

_Note: until all the built-in prompts have been documented, you can find each prompt name by looking for the `prompt_for` helpers' argument in the [init templates' source .js files](../tasks/init)._

## Overriding template files <a name="overriding-template-files" href="#overriding-template-files" title="Link to this section">⚑</a>
You can override any init template file, even the init template itself.

For example, the "jquery" init template exists inside of grunt at this path:

* [tasks/init/jquery.js](../tasks/init/jquery.js)

A set of jquery-template-specific rename rules exists at this path:

* [tasks/init/jquery/rename.json](../tasks/init/jquery/rename.json)

And any files to be copied by this template (because the template uses the `init.filesToCopy` and `init.copyAndProcess` methods), exist here:

* [tasks/init/jquery/root/](../tasks/init/jquery/root)

_Any_ of these files can be overridden via a referenced [grunt plugin](plugins.md) or tasks directory, OR via your [grunt.file.userDir](api_file.md) which is `%USERPROFILE%\.grunt\` on Windows, and `~/.grunt/` on OS X or Linux. This directory structure mimics grunt's internal directory structure.

So you can override any of the aforementioned things for a given init template `TEMPLATE` with these OS X / linux paths:

* `~/.grunt/tasks/init/TEMPLATE.js`
* `~/.grunt/tasks/init/TEMPLATE/rename.json`
* `~/.grunt/tasks/init/TEMPLATE/root/`

Or these Windows paths (`%USERPROFILE%` is generally your `Documents and Settings` directory):

* `%USERPROFILE%\.grunt\tasks\init\TEMPLATE.js`
* `%USERPROFILE%\.grunt\tasks\init\TEMPLATE\rename.json`
* `%USERPROFILE%\.grunt\tasks\init\TEMPLATE\root\`

If you wanted to change the `gruntfile` init template `grunt.js` file, you could copy grunt's own [tasks/init/gruntfile/root/grunt.js](../tasks/init/gruntfile/root/grunt.js) to `~/.grunt/tasks/init/gruntfile/root/grunt.js` (or the Windows equivalent), edit it as you see fit, and when you run `grunt init:gruntfile` grunt will use your file.

Assuming the template uses the `init.filesToCopy` and `init.copyAndProcess` methods, you can add any additional files into that "root" folder, with any arbitrarily-nested directory structure, and those files will be copied to the current directory when the init template is run.

For example, since the `gruntfile` init template is just two files, the [tasks/init/gruntfile.js](../tasks/init/gruntfile.js) template and the [tasks/init/gruntfile/root/grunt.js](../tasks/init/gruntfile/root/grunt.js) file-to-be-copied, you could completely change its behavior by overriding both of those files.

## Renaming or excluding template files <a name="renaming-or-excluding-template-files" href="#renaming-or-excluding-template-files" title="Link to this section">⚑</a>
If, for some reason, you want to rename or exclude files, you can edit the aforementioned `rename.json` which describes a map of `sourcepath` to `destpath` values. The `sourcepath` must be the path of the file-to-be-copied relative to the `root/` folder, but the `destpath` value can contain `{% %}` init templates, as in any init file, and describes what the destination path will be. See the `jquery` init template [rename.json](../tasks/init/jquery/rename.json) file for an example.

A few notes about `rename.json`:

* If `false` is specified for the `destpath` the file will not be copied.
* The `rename.json` file is _merged_ using `grunt.task.readDefaults` so it _overrides_ built-in values.

## Creating custom templates <a name="creating-custom-templates" href="#creating-custom-templates" title="Link to this section">⚑</a>
You create a custom template the exact same way you override init templates and their files, you just use a unique template name. in your userDir, just create a `~/.grunt/tasks/init/MYTEMPLATE.js` and any other relevant files. See the "Overriding template files" and "Renaming or excluding template files" sections for all the details.

## Defining an init template <a name="defining-an-init-template" href="#defining-an-init-template" title="Link to this section">⚑</a>

### exports.description <a name="exports-description" href="#exports-description" title="Link to this section">⚑</a>
This brief template description will be displayed along with the template name when the user runs `grunt init` or `grunt init:` to display a list of all available init templates.

```javascript
exports.description = descriptionString;
```

### exports.notes <a name="exports-notes" href="#exports-notes" title="Link to this section">⚑</a>
If specified, this optional extended description will be displayed before any prompts are displayed. This is a good place to give the user a little help explaining naming conventions, which prompts may be required or optional, etc.

```javascript
exports.notes = notesString;
```

### exports.warnOn <a name="exports-warnon" href="#exports-warnon" title="Link to this section">⚑</a>
If this optional (but recommended) wildcard pattern or array of wildcard patterns is matched, grunt will abort with a warning that the user can override with `--force`. This is very useful in cases where the init template could potentially override existing files.

```javascript
exports.warnOn = wildcardPattern;
```

While the most common value will be `'*'`, matching any file or directory, the [minimatch](https://github.com/isaacs/minimatch) wildcard pattern syntax used allows for a lot of flexibility. For example:

```javascript
exports.warnOn = 'grunt.js';        // Warn on a grunt.js file.
exports.warnOn = '*.js';            // Warn on any .js file.
exports.warnOn = '*';               // Warn on any non-dotfile or non-dotdir.
exports.warnOn = '.*';              // Warn on any dotfile or dotdir.
exports.warnOn = '{.*,*}';          // Warn on any file or dir (dot or non-dot).
exports.warnOn = '!*/**';           // Warn on any file (ignoring dirs).
exports.warnOn = '*.{png,gif,jpg}'; // Warn on any image file.

// This is another way of writing the last example.
exports.warnOn = ['*.png', '*.gif', '*.jpg'];
```

### exports.template <a name="exports-template" href="#exports-template" title="Link to this section">⚑</a>
While the `exports` properties are defined outside this function, all the actual init code is specified inside. Three arguments are passed into this function. The `grunt` argument is a reference to grunt, containing all the [grunt methods and libs](api.md). The `init` argument is an object containing methods and properties specific to this init template. The `done` argument is a function that must be called when the init template is done executing.

```javascript
exports.template = function(grunt, init, done) {
  // See the "Inside an init template" section.
};
```

## Inside an init template <a name="inside-an-init-template" href="#inside-an-init-template" title="Link to this section">⚑</a>
_(Documentation coming soon)_

<!--### The prompt helper <a name="the-prompt-helper" href="#the-prompt-helper" title="Link to this section">⚑</a>
EXPLAIN

```javascript
grunt.helper('prompt' [, defaults] [, options], done)
```

### The prompt_for helper <a name="the-prompt-for-helper" href="#the-prompt-for-helper" title="Link to this section">⚑</a>
EXPLAIN

```javascript
grunt.helper('prompt_for', name [, default])
```

### init.method <a name="init-method" href="#init-method" title="Link to this section">⚑</a>
EXPLAIN

```javascript
init.method()
```
-->

## Built-in prompts <a name="built-in-prompts" href="#built-in-prompts" title="Link to this section">⚑</a>
_(Documentation coming soon)_

See the [init task source](../tasks/init.js) for more information.
