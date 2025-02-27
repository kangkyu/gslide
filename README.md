# Gslide

Welcome to Gslide! This is an approach to build a Google Slides file for practical use.

## Installation

> Alternatively, replace this section with instructions to install your gem from git if you don't plan to release to RubyGems.org.

Install the gem and add to the application's Gemfile by executing:

```bash
bundle add gslide --github 'lininglink/gslide'
bundle install
```

## Usage

- Get a token with related scopes: `presentations` `presentations.readonly` `drive` `drive.readonly` `drive.file`.
- Get it from Google Developers [OAuth 2.0 Playground](https://developers.google.com/oauthplayground) for test.

```rb
token = "ya29.a0AXeO8..."
id = "113Xmx0YQc..."
editor = Gslide::Editor.new(token)
pres = Gslide::Presentation.new(id, auth: editor)
pres.get
#=> parsed json of the Google Slides file
```

```rb
editor = Gslide::Editor.new(token)
editor.insert_presentation(title: "Once upon a time")
#=> <Gslide::Models::Presentation:0x000000013e6d4108
#   @id="1itXwmlLbyTRa1QKhrsO16OhJPEJUK6eh2d1nqsQfuqY">

pres = _
pres.batch_update({
  requests: [
    {
      createSlide: {
        slideLayoutReference: {
          predefinedLayout: "BLANK"
        }
      }
    }
  ]
})

pres.get_slide_ids
#=> ["p", "SLIDES_API1463300837_0"]

pres.batch_update({
  requests: [
    {
      createImage: {
        url: "https://drive.usercontent.google.com/download?id=1fus5psRLzIJjG3A5GAfbqu22cdEczNZQ&authuser=0",
        elementProperties: {
          pageObjectId: "SLIDES_API1463300837_0",
          size: {
            height: { magnitude: 200, unit: "PT" },
            width: { magnitude: 300, unit: "PT" }
          },
          transform: {
            scaleX: 1,
            scaleY: 1,
            translateX: 100,
            translateY: 100,
            unit: "PT"
          }
        }
      }
    }
  ]
})
#=> true
```

## Development

After checking out the repo, run `bin/setup` to install dependencies. Then, run `rake test` to run the tests. You can also run `bin/console` for an interactive prompt that will allow you to experiment.

Install the gem (a local copy) and add to the application's Gemfile by executing:

```bash
bundle add gslide --path '../gslide'
```

To install this gem onto your local machine, run `bundle install`.

## Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/lininglink/gslide. This project is intended to be a safe, welcoming space for collaboration, and contributors are expected to adhere to the [code of conduct](https://github.com/lininglink/gslide/blob/master/CODE_OF_CONDUCT.md).

## License

The gem is available as open source under the terms of the [MIT License](https://opensource.org/licenses/MIT).

## Code of Conduct

Everyone interacting in the Gslide project's codebases, issue trackers, chat rooms and mailing lists is expected to follow the [code of conduct](https://github.com/lininglink/gslide/blob/master/CODE_OF_CONDUCT.md).
