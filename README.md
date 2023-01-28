# Identity-monad

identityMonad(value)
 .bind(k)
 .bind(j, j1, j2)
 .bind(i, i2)
.bind(h, h1, h2)
 .bind(g, g1, g2)
 .bind(f, f1, f2);
function identityMonad(value) {
 var monad = Object.create(null);
 
 // func should return a monad
 monad.bind = function (func, ...args) {
 return func(value, ...args);
 };
 // whatever func does, we get our monad back
 monad.call = function (func, ...args) {
 func(value, ...args);
 return identityMonad(value);
 };
 
 // func doesn't have to know anything about monads
 monad.apply = function (func, ...args) {
 return identityMonad(func(value, ...args));
 };
 // Get the value wrapped in this monad
 monad.value = function () {
 return value;
 };
 
 return monad;
};
