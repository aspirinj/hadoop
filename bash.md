## Check existence
```bash
if [ -z ${var+x} ]; then echo "var is unset"; else echo "var is set to '$var'"; fi
```

where `${var+x}` is a [parameter expansion](http://pubs.opengroup.org/onlinepubs/9699919799/utilities/V3_chap02.html#tag_18_06_02) which evaluates to nothing if `var` is unset, and substitutes the string `x` otherwise.

### Quotes Digression

Quotes can be omitted (so we can say `${var+x}` instead of `"${var+x}"`) because this syntax & usage guarantees this will only expand to something that does not require quotes (since it either expands to `x` (which contains no word breaks so it needs no quotes), or to nothing (which results in `[ -z ]`, which conveniently evaluates to the same value (true) that `[ -z "" ]` does as well)).

However, while quotes can be safely omitted, and it was not immediately obvious to all (it wasn't even apparent to [the first author of this quotes explanation](https://stackoverflow.com/users/2255628/destiny-architect) who is also a major Bash coder), it would sometimes be better to write the solution with quotes as `[ -z "${var+x}" ]`, at the very small possible cost of an O(1) speed penalty. The first author also added this as a comment next to the code using this solution giving the URL to this answer, which now also includes the explanation for why the quotes can be safely omitted.


### (Often) The wrong way

```
if [ -z "$var" ]; then echo "var is blank"; else echo "var is set to '$var'"; fi
```

This is often wrong because it doesn't distinguish between a variable that is unset and a variable that is set to the empty string. That is to say, if `var=''`, then the above solution will output "var is blank".

The distinction between unset and "set to the empty string" is essential in situations where the user has to specify an extension, or additional list of properties, and that not specifying them defaults to a non-empty value, whereas specifying the empty string should make the script use an empty extension or list of additional properties.

The distinction may not be essential in every scenario though. In those cases `[ -z "$var" ]` will be just fine.
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTUwMTk2Mjc2NF19
-->