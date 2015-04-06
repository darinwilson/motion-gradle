# motion-gradle

motion-gradle allows RubyMotion projects to integrate with the
[Gradle](http://gradle.apache.org/) dependency manager.


## Installation

You need to have gradle installed: 

```
$ brew install gradle
```

And the gem installed: 

```
$ [sudo] gem install motion-gradle
```

Or if you use Bundler:

```ruby
gem 'motion-gradle'
```

You also need to install `Extras/Android Support Repository` the Android SDK Manager gui.

![android-sdk-manager](https://raw.github.com/jaffeux/motion-gradle/images/android-sdk-manager.png)


## Setup

1. Edit the `Rakefile` of your RubyMotion project and add the following require
   lines:

   ```ruby
   require 'rubygems'
   require 'motion-gradle'
   ```

2. Still in the `Rakefile`, set your dependencies

  ```ruby
  Motion::Project::App.setup do |app|
    # ...
    app.gradle do
      dependency 'com.mcxiaoke.volley', :artifact => 'library', :version => '1.0.10'
      dependency 'commons-cli'
      dependency 'ehcache', :version => '1.2.3'
    end
  end
  ```

  * :version will default to latest: +

  * :artifact will default to dependency name


## Configuration

If the `gradle` command is not in your path, you can configure it:

```ruby
Motion::Project::App.setup do |app|
  # ...
  app.gradle.path = '/some/path/gradle'
end
```

You can also add other repositories :

```ruby
Motion::Project::App.setup do |app|
  # ...
  app.gradle do
    repository 'https://bintray.com/bintray/jcenter'
    repository 'http://dl.bintray.com/austintaylor/gradle'
  end
end
```

## Tasks

To tell motion-gradle to download your dependencies, run the following rake
task:

```
$ [bundle exec] rake gradle:install
```

After a `rake:clean:all` you will need to run the install task agin.

That’s all.