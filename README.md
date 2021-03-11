# utl-rounding-three-decimal-digits-to-the-nearest-tenth-and-addin-a-zero
Rounding three decimal digits to the nearest tenth and adding a zero on the end

    Rounding three decimal digits to the nearest tenth and adding a zero on the end

      Problem

            OLD           NEW

          14543.567     14543.570
          647473.543    647473.540

    * messing with decimal arithmetic in a binary world can be dangerous;
    * best to work with integers because addition and mutiplication of integers has
    closure in both domains;

    Inspired by
    https://tinyurl.com/t94xxynj
    https://stackoverflow.com/questions/66441914/how-to-formatting-numeric-values-to-the-3rd-digit-whilst-it-evens-it-to-2nd-digi

    *_                   _
    (_)_ __  _ __  _   _| |_
    | | '_ \| '_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    ;

    data have;
     informat old $16.;
     input old;
    cards4;
    14543.567
    647473.543
    111111.111
    ;;;;
    run;quit;

    *
     _ __  _ __ ___   ___ ___  ___ ___
    | '_ \| '__/ _ \ / __/ _ \/ __/ __|
    | |_) | | | (_) | (_|  __/\__ \__ \
    | .__/|_|  \___/ \___\___||___/___/
    |_|
    ;

    data want;

     set have;
     length old new $16;

     int=round(input(compress(old,'.'),best12.),10); * I think this is safe - integer processing;
     intchr=put(int,16.); * still integer;

     new=cats(substr(intchr,1,length(intchr)-2),'.',substr(intchr,length(intchr)-2));
     * I hesitate to turn want into a float because
       111111.110 does not have an exact binary representation;

     * need to know what will be done with your output;
     * give he/she the char value and let them decide to estimate it with a float;

     drop int intchr;

    run;quit;

    *            _               _
      ___  _   _| |_ _ __  _   _| |_
     / _ \| | | | __| '_ \| | | | __|
    | (_) | |_| | |_| |_) | |_| | |_
     \___/ \__,_|\__| .__/ \__,_|\__|
                    |_|
    ;

    Up to 40 obs WORK.WANT total obs=3

    Obs       OLD            NEW

     1     14543.567     145435.570
     2     647473.543    6474735.540
     3     111111.111    1111111.110


