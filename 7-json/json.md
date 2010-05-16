!SLIDE subsection

# Step7: Store the "poos"

!SLIDE bullets incremental

# Considerations:

* I need to store 3 languages
* How should I "canonicalise" pinyin?
* I don't want to use SQL

!SLIDE bullets

# Schema:
* english: string
* zhongwen: string
* pinyin: string

!SLIDE bullets incremental

# Pinyin:
* Nǐ hǎo ma?
* VS
* Ni3 hao3 ma?

!SLIDE

## they both look a bit crap

!SLIDE

# Zhi3 yong4 shu4 zi4

!SLIDE

# noSQL?

!SLIDE

## Let's just use JSON
(we'll think about proper storage later)

!SLIDE code

    @@@ ruby
    [{"id": 2,
    "english": "How's your bum?",
    "zhongwen": "你的屁股怎么样？",
    "pinyin": "Ni3de pi4gu zen3me yang4?"
    }]

    require 'json'
    POSTS = JSON.parse(File.read("posts.json"))
    
    <% POSTS.each do |post| %>
      <p><%= post["english"] %></p>
    <% end %>
    
!SLIDE

# we can fake dynamism

!SLIDE code

    @@@ ruby
    POSTS = JSON.parse(File.read("posts.json"))
    
    get "/" do
      @posts = POSTS
      erb :index
    end
    
    get "/posts/:id" do
      @posts = POSTS.select{|p| p["id"] == params[:id].to_i}
      erb :index
    end
