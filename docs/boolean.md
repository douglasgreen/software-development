# Boolean

Don't use Boolean arguments because then your functions are called like this:

save($file, true, false, false, true);

What do those mean? You also have to pass each flag in order, which are easily
confused. Instead, use integer flags.

save($file, OVERWRITE | DEFER);
