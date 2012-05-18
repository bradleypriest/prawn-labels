# Prawn/Labels: A simple helper to generate labels for Prawn PDFs

Prawn/Labels takes the guess work out of generating labels using Prawn ~> 0.11.1

## Install

```bash
$ gem install prawn-labels
```

## Usage

We've tried to make generating labels as simple as possible with Prawn::Labels.
If you have an object which responds to `each`, then you're in business.

### Create and save a PDF file

```ruby
require 'prawn/labels'

names = ["Jordan", "Chris", "Jon", "Mike", "Kelly", "Bob", "Greg"]

Prawn::Labels.generate("names.pdf", names, :type => "Avery5160") do |pdf, name|
  pdf.text name
end
```

This creates a document with a name from the names array in each label. The labels will be formatted for Avery 5160 labels. Formats are defined in the `prawn/labels/types.yaml` file, or by [loading a custom hash or yaml file](#custom-label-types)

For a full list of examples, take a look in the `examples` folder.

### Render a PDF file and send to browser

```ruby
labels = Prawn::Labels.render(names, :type => "Avery5160") do |pdf, name|
  pdf.text name
end

send_data labels, :filename => "names.pdf", :type => "application/pdf"
```

### Scale text to fit label

```ruby
Prawn::Labels.generate( "names.pdf", names, :type => "Avery5160",
                        :shrink_to_fit => true) do |pdf, name|
  pdf.text name
end
```

### Create custom label types

If the label type you need to use isn't defined in `prawn/labels/types.yaml`
file, you can define and load your own.

```ruby
Prawn::Labels.types = '/path/to/custom/types.yaml'

Prawn::Labels.generate("names.pdf", names, :type => "Custom123") do |pdf, name|
  pdf.text name
end
```

or using a hash:

```ruby
Prawn::Labels.types = {
  "QuarterSheet" => {
    "paper_size" => "A4",
    "columns"    => 2,
    "rows"       => 2
}}

Prawn::Labels.generate("names.pdf", names, :type => "QuarterSheet") do |pdf, name|
  pdf.text name
end
```

## Contributors

- [Jordan Byron](http://jordanbyron.com)
- [David Speake](mailto:david@verycleverstuff.co.uk)
- [Carlo Biedenharn](mailto:cbieden@mit.edu)
- [Forrest Zeisler](https://github.com/forrest)
- [Jack Twilley](https://github.com/mathuin)
- [Ori Pekelman](https://github.com/OriPekelman)