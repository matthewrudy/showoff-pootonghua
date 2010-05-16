!SLIDE subsection

# Step8: Heroku

!SLIDE

# I already have a couple of VPSs

!SLIDE

## could just configure passenger

!SLIDE code

    @@@ ruby
    # config.ru
    
    require 'poos'
    run Sinatra::Application

!SLIDE

## I'd rather try something new

!SLIDE

# Heroku

!SLIDE commandline

    @@@ bash
    $ gem install heroku
    $ heroku create
    $ git push heroku master
    
!SLIDE code

    @@@
    matthew@RuPro:~/code/poopoo$ git push heroku 
    -----> Heroku receiving push
    -----> Gemfile detected, running Bundler
           All dependencies are satisfied
           Locking environment
    -----> Sinatra app detected
           Compiled slug size is 1.6MB
    -----> Launching........ done
           http://simple-sword-52.heroku.com deployed to Heroku

!SLIDE

# DONE

