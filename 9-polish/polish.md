!SLIDE subsection

# Step9: Polish

!SLIDE

# add caching

!SLIDE code

    @@@ ruby
    def cache!
      etag "v#{VERSION}p#{POSTS.hash}" # version + hash of data
      response["Cache-Control"] = "max-age=300, public" # 5 minutes
    end
    
    get "/" do
      cache!
      @posts = POSTS
      erb :index
    end
    
!SLIDE

# use your own domain

!SLIDE code

    @@@ ruby
    BASE_URI = URI.parse("http://pootonghua.com")
    
    before do
      if env["HTTP_HOST"] =~ /heroku\.com$/
        redirect BASE_URI.merge(env["PATH_INFO"]).to_s
      end
    end
    
!SLIDE

# Make the JSON more objecty

!SLIDE code

    @@@ ruby
    class Poo

      def self.all
        POSTS.map{|hash| Poo.new(hash)}
      end

      def self.find(id)
        self.all.detect{|p| p.id == id.to_i}
      end
      
      def initialize(hash)
        @hash = hash
      end
      attr_reader :hash

      [:id, :english, :zhongwen, :pinyin].each do |key|
        define_method(key) do
          hash[key.to_s]
        end
      end
    end
    
!SLIDE

## But I still need to deploy if I want to add a "poo"
    