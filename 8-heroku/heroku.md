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
    
!SLIDE

# DONE