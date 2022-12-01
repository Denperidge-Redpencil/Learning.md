Some commands & principles I've learned from the course that I might want to have in an overview!

## Design principles
### The rule of Least Power
For Ember, (I think) it boils down to this:
- You should use the least powerful language to fix problems
- No JavaScript in templating/handlebars means that future updates will have minimal breaking changes

Also see 11:30 in this [Emberweekend episode](https://emberweekend.com/episodes/the-rule-of-least-power/) and the [W3C piece on it](https://www.w3.org/2001/tag/doc/leastPower.html).

### Handlebars' fail-softness
undefined/null properties get ignored in Handlebars. This gives cleaner output and less conditional code, but is something to keep in mind when debugging.

## Commands


Thanks to [Rock And Roll with Ember Octane](https://balinterdi.com/rock-and-roll-with-emberjs/)