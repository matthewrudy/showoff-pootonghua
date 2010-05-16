!SLIDE subsection

# Step6: Sinatra

!SLIDE incremental bullets

# Sinatra
* been around for a while
* minimal API
* minimal bloat

!SLIDE code

    @@@ ruby
    require 'sinatra'
    
    get '/' do
      erb :index
    end
