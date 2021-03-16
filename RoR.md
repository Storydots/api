# **RoR example snippet for retrieving a tag**

```ruby
require 'uri'
require 'net/http'
require 'json'
class CaseSensitiveGet < Net::HTTP::Get
    def initialize_http_header(headers)
      @header = {}
      headers.each{|k,v| @header[k.to_s] = [v] }
    end
  
    def [](name)
      @header[name.to_s]
    end
  
    def []=(name, val)
      if val
        @header[name.to_s] = [val]
      else
        @header.delete(name.to_s)
      end
    end
  
    def capitalize(name)
      name
    end
  end
  
class StoryDots
def initialize
    # story_dots = Webhook.story_dots.first
    @basic_end_point = "https://api.storydots.app"
    @api_key = story_dots.app_secret
end
def get_url_link
    puts @api_key
    end_point = "#{@basic_end_point}/tag"
    uri = URI.parse("#{end_point}")
    # request = Net::HTTP::Get.new(uri)
    request = CaseSensitiveGet.new(uri)
    request["cache-control"] = "no-cache"
    request["x-api-key"] = @api_key
    req_options = {
      use_ssl: uri.scheme == "https",
      read_timeout: 7,
      }
    puts uri.hostname
    puts uri.port
    response = Net::HTTP.start(uri.hostname, uri.port, req_options) do |http|
     http.read_timeout = 2
     http.request(request)
    end
    # return JSON.parse(response.body)
    return response.code
end
def get_qr(tag_code)
    end_point = "#{@basic_end_point}/qr/#{tag_code}"
    uri = URI.parse("#{end_point}")
    request = Net::HTTP::Get.new(uri)
    request["Accept"] = "image/png"
    req_options = {
      use_ssl: uri.scheme == "https",
      read_timeout: 7,
      }
    response = Net::HTTP.start(uri.hostname, uri.port, req_options) do |http|
     http.read_timeout = 2
     http.request(request)
    end
    return response.body
end
end
sd = StoryDots.new
puts sd.get_url_link
```
