# Ltsv

LTSV: A Parser / Dumper for Labelled Tab-Separated Values (LTSV)

## Installation

Add this line to your application's Gemfile:

    gem 'ltsv'

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install ltsv

## Usage

At first, you should require ltsv:

    require 'ltsv'

In addition, if you manage gems with bundler, you should add the statement below into your Gemfile:

    gem 'ltsv'


### parsing LTSV

    # parse string
    string = "label1:value1\tlabel2:value2"
    values = LTSV.parse(string) # => {:label1 => "value1", :label2 => "value2"}

    # parse via stream
    # content: as below
    # label1_1:value1_1\tlabel1_2:value1_2
    # label2_1:value2_1\tlabel2_2:value2_2
    stream = File.open("some_file.ltsv", "r")
    values = LTSV.parse(stream)
    # => [{:label1_1 => "value1_2", :label1_2 => "value1_2"},
    #     {:label2_1 => "value2_2", :label2_2 => "value2_2"}]

Current limitation: parsed string should be in one line. If you include any special chars that may affect to the processing( "\r", "\n", "\t", "\\"), you should properly escape it with backslash.

### loading LTSV file

    # parse via path
    values = LTSV.parse("some_path.ltsv")

    # parse via stream
    stream = File.open("some_file.ltsv", "r")
    values = LTSV.load(stream) # => same as LTSV.parse(stream)

### dumping into LTSV

    value = {label1: "value1", label2: "value2"}
    dumped = LTSV.dump(value) # => "label1:value1\tlabel2:value2"

Dumped objects should respond to :to_hash.

### Author and Contributors

* Author
  * Naoto "Kevin" IMAI TOYODA <condor1226@github.com>

* Contributors
  * Naoto SHINGAKI <https://github.com/naoto/>
  * chezou <https://github.com/chezou>

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request
