!SLIDE  

## `ruby -c`: Syntax checking

	$ echo "class Foo" | ruby -c
	  -:1: syntax error, unexpected $end
	
	$ echo "class Foo; end" | ruby -c
	  Syntax OK

!SLIDE   small

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

!SLIDE  

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

!SLIDE  

## underscore in `irb`

	# %w(a b c).map(&:succ)
	["b", "c", "d"]
	
	# _
	["b", "c", "d"]
	
	# letters = _
	["b", "c", "d"]

!SLIDE  

## string concatenation

	# "ab" + "cd"
	"abcd"

	# "ab" "cd"
	"abcd"

!SLIDE 

## string interpolation, normal

	@@@ ruby
	a = 2
	b = "1#{a}3"
	p b

- `123`

!SLIDE 

## string interpolation, also normal

	@@@ ruby
	@a = 5
	b = "4#{@a}6"
	p b

- `456`

!SLIDE  small

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

!SLIDE 

## interpolate into symbols

	@@@ ruby
	p :this_is_a_symbol.object_id
	
	klass = "symbol"
	p :"this_is_a_#{klass}".object_id

- `333788`
- `333788`

!SLIDE 

## string delimiters

	@@@ ruby
	"String!"
	'String!'
	%{String!}
	%|String!|
	%`String!`
	%;String!;

!SLIDE 

## `String#*`

	# "*" * 80
	********************************************************************************

!SLIDE  

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

!SLIDE  

## `redo`

	# s = ''
	""
	
	# 1.upto(5) { |i| s << i.to_s; redo if s.size < 3 }
	1
	
	# s
	"1112345"

!SLIDE

## pulling elements out of arrays

	# args = [1, 2, 3]
	# first, *rest = args
	# first
	1

	# rest
	[2, 3]

!SLIDE  

## splat arguments, anywhere (1.9+)

	# def foo(*args); p args; end
	# foo(1, 2, 3, 4)
	[1, 2, 3, 4]
	
	# def bar(first, *args); p first; p args; end
	# bar(1, 2, 3, 4)
	1
	[2, 3, 4]
	
	# def baz(first, *args, last); p first; p args; p last; end
	# baz(1, 2, 3, 4)
	1
	[2, 3]
	4

!SLIDE  small

## destructuring arrays

	@@@ ruby
	def touch_down
	  yield [3, 7]
	  puts "touchdown!"
	end
	
	touch_down do |(first_down, second_down)|
	  puts "#{first_down} yards on the run"
	  puts "#{second_down} yards passed"
	end

- `3 yards on the run`
- `7 yards passed`
- `touchdown!`

!SLIDE  

## `Enumerable#any? / #all?`

	# [false, false, true].any?
	true
	
	# [false, false, nil].any?
	false
	
	# [true, true, true].all?
	true
	
	# [true, true, false].all?
	false

!SLIDE   small

## `Hash#new` with a block

	# smash = Hash.new { |hash, key| hash[key] = "a #{key} just got SMASHED!" }
	{}
	
	# smash[:plum] = "cannot smash."
	{:plum=>"cannot smash."}
	
	# smash[:watermelon]
	{:plum=>"cannot smash.", :watermelon=>"a watermelon just got SMASHED!"}

!SLIDE  

## `Hash::[]`

	# Hash[:apples, 3, :bananas, 2]
	{:apples=>3, :bananas=>2}
	
	# Hash[[:apples, 3, :bananas, 2] * 300_000]
	SystemStackError: stack level too deep

[Ruby bug](http://redmine.ruby-lang.org/issues/5719) warning!

!SLIDE  

## `j` and `jj` (1.9+)

	# require 'json'
	# h = {a: 1, b:2}
	{:a=>1, :b=>2}
	
	# j(h)
	{"a":1,"b":2}
	
	# jj(h)
	{
	  "a": 1,
	  "b": 2
	}
