# [christoph neuroth](http://programm.froscon.de/2014/events/1462.html)

* "Testing shows the presence, not the absence of bugs" (Diijkstra)
* [slides](http://www.slideshare.net/chris089/propertybased2014-0823propertybased-testingfroscon9)

# [testing with properties](https://github.com/phadej/jsverify)

* not to be confused with properties on JavaScript objects
* specify a property that holds for all/specified inputs
* instead of finding a proof, test random inputs
* similar to contracts
* examples uses jsverify, other implementations are available

# describing a property

## as a human

"Whatever number we pass to abs, it should return a number greater or equal 0"

## as a programmer

### first try

    var p = require('jsverify');
    p.check(p.forall(p.number(), function (x) {
        var actual = Math.abs(x);
        return typeof actuall === 'number' && actual >= 0;
    }));

### why not?

    var p = require('jsverify');
    p.check(p.forall(p.number(), function (x) {
        return Math.abs(x) >= x;
    }));

# reusable properties

    var is_idempotent = function (generator, fn) {
        return p.forall(generator, function (x) {
            return _.isEqual(fn(fn(s)), fn(s));
        });
    };
    p.assert(is_idempotent(p.array(), _.compact));
    p.assert(is_idempotent(p.array(), _.uniq));

# shrinking counterexampls

    p.assert(p.forall(p.array(p.integer()), function (1) {
        return _.all(1, function (n) { return n!=3; });
    }));

# common use cases

    f(x) >= y   // asserting the functions range
    f(x) === f(f(x));   // idempotence
    a(x) === b(x);  // regression test for reimplementation
    new C1().f(x) === new C2().f(x);    // closely related
    new C(c1).f(x) === new C(c2).f(x);  // closely related
    (max(a, b) === max(b, a));    // commutativity
    (zoom(zoom(img, n), -n) === img);    // invertibility

# conclusion

* finding good properties makes you think harder
* very functional style, but should work on testing oo code
* not a replacement for TDD using examples
* but can be used to help finding missed edge cases
* best for unit testing (because of high number of test cases)
* also good for verifying assumtpions on 3dparty code
