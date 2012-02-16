# arrrrug_2012_02

!SLIDE

# relativity
# EntityMap

## @peter_v

!SLIDE

# "7 to 5"

``` ruby
Time.new # => 2012-02-15 21:56:50 0100
require 'date'
Date.new # => #<Date: -4712-01-01 ((0j,0s,0n),+0s,2299161j)>
DateTime.new # => #<DateTime: -4712-01-01T00:00:00+00:00 ((0j,0s,0n),+0s,2299161j)>
"7 to 5" # => "7 to 5" ??
```
!SLIDE

# relativity

```
require 'relativity'
start_at = DayTime.new("9") # => 09:00:00
end_at = DayTime.new("12:35:30") # => 12:35:30
now = DayTime.new # => 22:09:42

seven_to_five = DayTimeRange.new("7 to 17", :separator => " to ")
# => 07:00:00 to 17:00:00
night_shift = DayTimeRange.new("21:55 until 6:55:30")
# => 21:55:00 until 06:55:30
```
!SLIDE

# With a Background Image

}}} images/test.png
