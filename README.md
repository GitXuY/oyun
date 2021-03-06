README for Oyun
===============

See the Oyun website: http://charlespence.net/oyun/

Oyun is a program you can use to run tournaments between various strategies
playing normal-form games such as the prisoner's dilemma.  The classic work on
such tournaments is Robert Axelrod's *The Evolution of Cooperation,* and Oyun
takes much inspiration from such tournaments.

Oyun allows you to create players, using a simple finite state machine syntax,
and these players then compete in tournaments -- either one-off, round-robin
tournaments or "evolutionary" tournaments in which strategies compete to
increase their proportion in a "population" over a number of generations.


Installation
------------

In general, if you have an appropriate version of wxWidgets and a normal set of
userspace tools (such as on Linux, OS X, or MinGW), you should just be able to
execute the usual `configure`, `make`, `make install` combo.

In detail, the compilation of Oyun requires:

* wxWidgets (preferably version 2.9.2+, and preferably statically-linked)
* Doxygen (for the compilation of the source-code docs)
* pandoc (http://johnmacfarlane.net/pandoc/, for compilation of the manual)
* pdflatex (http://tug.org/texlive/, for compilation of the manual)
* zip (http://www.info-zip.org/Zip.html, for compilation of the manual)


More documentation
------------------

For information about Oyun development, as well as detailed documentation, see 
the Oyun website at http://charlespence.net/oyun/.


Copying
-------

    Copyright (C) 2004-2011 by Charles Pence
    charles@charlespence.net

    This file is part of Oyun.

    Oyun is free software: you can redistribute it and/or modify
    it under the terms of the GNU General Public License as published by
    the Free Software Foundation, either version 3 of the License, or
    (at your option) any later version.

    Oyun is distributed in the hope that it will be useful,
    but WITHOUT ANY WARRANTY; without even the implied warranty of
    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
    GNU General Public License for more details.

    You should have received a copy of the GNU General Public License
    along with Oyun.  If not, see <http://www.gnu.org/licenses/>.

