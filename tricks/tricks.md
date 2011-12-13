!SLIDE commandline incremental

## `ruby -c`: Syntax checking

	$ echo "class Foo" | ruby -c
	  -:1: syntax error, unexpected $end
	
	$ echo "class Foo; end" | ruby -c
	  Syntax OK

!SLIDE commandline incremental small

## `ruby -w`: Indent checking (1.9+)

	$ cat bad.rb
	class Foo
	  def bar
	    if false
	      puts "LOL"
	  end
	end

	$ ruby -w bad.rb
	bad.rb:5: warning: mismatched indentations at 'end' with 'if' at 3
	bad.rb:6: warning: mismatched indentations at 'end' with 'def' at 2
	bad.rb:6: syntax error, unexpected $end, expecting keyword_end

!SLIDE commandline incremental

## `ruby -p, -e, -i`

	$ echo matz | ruby -p -e '$_.tr! "a-z", "A-Z"'
	MATZ
	$ echo matz > /tmp/junk
	$ cat /tmp/junk
	matz
	$ ruby -p -i.bak -e '$_.upcase!' /tmp/junk
	$ cat /tmp/junk
	MATZ
	$ cat /tmp/junk.bak
	matz

!SLIDE

## underscores in numbers

	@@@ ruby
	1_000.times do
	  puts "ROFL!"
	end

	(1..300_000_000).each do |n|
	  puts "LMAO!"
	end

!SLIDE commandline incremental

## underscore in `irb`

	# %w(a b c).map(&:succ)
	["b", "c", "d"]
	
	# _
	["b", "c", "d"]
	
	# letters = _
	["b", "c", "d"]

!SLIDE commandline incremental

## string concatenation

	# "ab" + "cd"
	"abcd"

	# "ab" "cd"
	"abcd"

!SLIDE incremental

## string interpolation, normal

	@@@ ruby
	a = 2
	b = "1#{a}3"
	p b

- `123`

!SLIDE incremental

## string interpolation, also normal

	@@@ ruby
	@a = 4
	b = "5#{@a}6"
	p b

- `123`

!SLIDE incremental small

## string interpolation, WTF?

	@@@ ruby
	@a = 8
	b = "#@a"
	c = "7#@a"
	d = "7#@a9"
	p b
	p c
	p d

- `8`
- `78`
- `7`

!SLIDE incremental

## interpolate into symbols

	@@@ ruby
	p :this_is_a_symbol.object_id
	
	klass = "symbol"
	p :"this_is_a_#{klass}".object_id

- `333788`
- `333788`

!SLIDE incremental

## string delimiters

	@@@ ruby
	"String!"
	'String!'
	%{String!}
	%|String!|
	%`String!`
	%;String!;

!SLIDE commandline

## `String#*`

	# "*" * 80
	********************************************************************************

!SLIDE

## `begin/rescue/else/end`

!SLIDE

## `throw/catch`

!SLIDE commandline incremental

## `DATA` and `__END__`

	$ cat data.rb
	p YAML.load(DATA.read)[ARGV.first]
	__END__
	foo: "Bar"
	baz: "LOL!"

	$ ruby -ryaml data.rb
	nil
	
	$ ruby -ryaml data.rb foo
	"Bar"
	
	$ ruby -ryaml data.rb bar
	"LOL!"

!SLIDE commandline incremental

## `redo`

	# s = ''
	""
	
	# 1.upto(5) { |i| s << i.to_s; redo if s.size < 3 }
	1
	
	# s
	"1112345"

!SLIDE

## splat arguments, anywhere (1.9+)

!SLIDE

## destructuring arrays

!SLIDE

## pulling elements out of arrays

!SLIDE

## `Enumerable#any? / #all?`

!SLIDE

## `Hash#fetch`

!SLIDE

## `Hash#new` with a block

!SLIDE

## `Hash::[]`

!SLIDE

## `Array#sort_by`

!SLIDE

## `String#present?` (Rails only)

!SLIDE

## `j` and `jj` (1.9+)

    require 'json'
    h = {a:1,b:2}
    j(h); jj(h)
*

!SLIDE

## `begin/rescue/else/end`

!SLIDE

## `throw/catch`

!SLIDE

## `DATA` and `__END__`

!SLIDE

## `redo`

    >> s = ''
    => ""
    >> 1.upto(5) { |i| s << i.to_s; redo if s.size < 3 }
    => 1
    >> s
    => "1112345"

!SLIDE

## splat arguments, anywhere (1.9+)

!SLIDE

## destructuring arrays

!SLIDE

## pulling elements out of arrays

!SLIDE

## `Enumerable#any? / #all?`

!SLIDE

## `Hash#fetch`

!SLIDE

## `Hash#new` with a block

!SLIDE

## `Hash::[]`

!SLIDE

## `Array#sort_by`

!SLIDE

## `String#present?` (Rails only)

!SLIDE

## `j` and `jj` (1.9+)

    require 'json'
    h = {a:1,b:2}
    j(h); jj(h)

