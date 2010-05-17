!SLIDE subsection

# Step11: Mongoid

!SLIDE

# ActiveRecord-ish interface to Mongo

!SLIDE code

    @@@ bash
    # Gemfile
    gem "mongoid", "2.0.0.beta4"
    gem "bson_ext", "0.20.1"
    
!SLIDE code

    @@@ ruby
    # phrase.rb
    class Phrase
      include Mongoid::Document
      include Mongoid::Timestamps

      field :english
      field :zhongwen
      field :pinyin
      
      validates_presence_of :english, :zhongwen, :pinyin
    end

!SLIDE

## but we get an id like "4bf003ce1d2bde1b6f000002"

!SLIDE

## doesn't work with our "/posts/12" model

!SLIDE

# use a "permalink" instead

!SLIDE code

    @@@ ruby
    field :permalink
    index :permalink, :unique => true

    validates_presence_of :permalink

    before_create :set_permalink
    def set_permalink
      self.permalink ||= self.english.strip.gsub(
        /['"]+/, "").gsub(/\W+/, "-").gsub(
          /-$/, "").downcase
    end
    
!SLIDE code

    @@@ ruby
    # app.rb
    get "/posts/:permalink" do
      @post = Phrase.first(
        :conditions => {
          :permalink => params[:permalink]})
      erb :show
    end

!SLIDE

## /posts/2
## becomes
## /posts/we-were-just-talking-about-you