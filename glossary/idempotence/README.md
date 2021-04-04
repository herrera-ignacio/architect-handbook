# Idempotence

A function `f` with side effects is said to be indempotent under sequential composition `f; f` if, when called twice with the same list of arguments, the __second call has no side effects and returns the same value as the first call__ (assuming no other procedures were called between the end of the first call and the start of the second call).
