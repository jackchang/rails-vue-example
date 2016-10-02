# Rails Vue example

A simple starter project to use Vue.js with Ruby on Rails 4

A Vue component to show hours and minutes:

![Rails Vue example](https://raw.githubusercontent.com/blocknotes/rails-vue-example/master/screenshot.png "Rails Vue example")

## Rails & Vue setup

- Create a basic web app:
```sh
rails _4.2.5.2_ new rails-vue-example -j --skip-spring --skip-turbolinks
```

- Create a controller (ex. *home*), a view (ex. *home/index*) and setup a default route (ex. *home#index*)

- Setup *bower-rails*:
```sh
rails g bower_rails:initialize
echo -e "\nasset 'vue'" >>! Bowerfile
rake bower:update
```

- Add *vue.js* reference to *application.js* (or .coffee):
```ruby
//= require vue/dist/vue
```

## Vue components setup

- app/assets/javascripts/application.js: add
```ruby
//= require components_init
```

- app/assets/stylesheets/application.css: add
```ruby
*= require components_init
```

- app/views/layouts/application.html.slim: move in the end of body tag:
```ruby
= javascript_include_tag 'application'
```

- config/assets/initializers: add:
```ruby
Rails.application.config.assets.paths << Rails.root.join( 'app', 'views', 'components' )
```

- app/views/components/components_init.css: content:
```css
/*
 *= require_tree .
 */
```

- app/views/components/components_init.js: content:
```javascript
//= require_tree .
```

## Usage

- app/assets/javascripts/init.js: init the vue app:
```javascript
new Vue({
  el: '#app'
});
```

- app/views/home/someview.html.slim: add an `#app` block with a custom tag inside
```slim
#app
  a-clock init-hour="12" init-min="25"
```

- app/views/components/clock/: create a new component with *clock.sass*, *clock.js.erb*, *clock.html.slim*

## Notes

- Slim templates are rendered when the asset pipeline is precompiled, so we need to avoid to call server side function to fetch data; instead we can use AJAX to load data remotely for example using [vue-resource](https://github.com/vuejs/vue-resource).
