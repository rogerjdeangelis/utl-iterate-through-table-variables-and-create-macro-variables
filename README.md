# utl-iterate-through-table-variables-and-create-macro-variables
Iterate through table variables and create macro variables
    Iterate through table variables and create macro variables

    github
    https:          //tinyurl.com/y6wuys6p
    https://github.com/rogerjdeangelis/utl-iterate-through-table-variables-and-create-macro-variables

    macros
    https://tinyurl.com/y9nfugth
    https://github.com/rogerjdeangelis/utl-macros-used-in-many-of-rogerjdeangelis-repositories

    github
    https://github.com/rogerjdeangelis/utl_create_many_macro_variables

    SAS-L  (related to)
    https://listserv.uga.edu/cgi-bin/wa?A2=SAS-L;85520750.2005a

       Three solutions
              a. do_over
              b. macro fetch
              c. datastep
     *
     _                   _
    (_)_ __  _ __  _   _| |_
    | | '_ \| '_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    ;
    * this is what your univariate output;

    * just in case the global variables already exist - no relly needed;
    %symd el PCT_10 PCT_20 PCT_30 PCT_40 PCT_50 PCT_60 PCT_70 PCT_80 PCT_90;

    * This is what the output of your univariate looks like;
    data have;
    input
     PCT_10 PCT_20 PCT_30 PCT_40 PCT_50 PCT_60 PCT_70 PCT_80 PCT_90;
    cards4;
    118 128 136 143 150 158 167 177 191
    ;;;;
    run;quit;

    *            _               _
      ___  _   _| |_ _ __  _   _| |_
     / _ \| | | | __| '_ \| | | | __|
    | (_) | |_| | |_| |_) | |_| | |_
     \___/ \__,_|\__| .__/ \__,_|\__|
                    |_|
    ;
     %put _user_;
    GLOBAL PCT_10 118
    GLOBAL PCT_20 128
    GLOBAL PCT_30 136
    GLOBAL PCT_40 143
    GLOBAL PCT_50 150
    GLOBAL PCT_60 158
    GLOBAL PCT_70 167
    GLOBAL PCT_80 177
    GLOBAL PCT_90 191
    *          _       _   _
     ___  ___ | |_   _| |_(_) ___  _ __  ___
    / __|/ _ \| | | | | __| |/ _ \| '_ \/ __|
    \__ \ (_) | | |_| | |_| | (_) | | | \__ \
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|___/
                   _
      __ _      __| | ___     _____   _____ _ __
     / _` |    / _` |/ _ \   / _ \ \ / / _ \ '__|
    | (_| |_  | (_| | (_) | | (_) \ V /  __/ |
     \__,_(_)  \__,_|\___/___\___/ \_/ \___|_|
                        |_____|
    ;
    %array(pcts,values=1-9);

    data _null_;
       set have;
       %do_over(pcts,phrase=%str(
          call symputx("pct_?0", pct_?0);
       ));
    run;quit;

    * if you want the generated code;
    data _null_;
       %do_over(pcts,phrase=%str(put "
          call symputx('pct_?0', pct_?0)"  /;
       ));
    run;quit;


    call symputx('pct_10', pct_10)
    call symputx('pct_20', pct_20)
    call symputx('pct_30', pct_30)
    call symputx('pct_40', pct_40)
    call symputx('pct_50', pct_50)
    call symputx('pct_60', pct_60)
    call symputx('pct_70', pct_70)
    call symputx('pct_80', pct_80)
    call symputx('pct_90', pct_90)


    *_                                          __      _       _
    | |__     _ __ ___   __ _  ___ _ __ ___    / _| ___| |_ ___| |__
    | '_ \   | '_ ` _ \ / _` |/ __| '__/ _ \  | |_ / _ \ __/ __| '_ \
    | |_) |  | | | | | | (_| | (__| | | (_) | |  _|  __/ || (__| | | |
    |_.__(_) |_| |_| |_|\__,_|\___|_|  \___/  |_|  \___|\__\___|_| |_|

    ;
    * just in case the global variables and array  already exist - no relly needed;
    %symd el PCT_10 PCT_20 PCT_30 PCT_40 PCT_50 PCT_60 PCT_70 PCT_80 PCT_90;
    %arraydelete(pcts);


    %array(pcts,values=1-9);

       %let dsid=%sysfunc(open(have,i));

       %syscall set(dsid);

       %let rc=%sysfunc(fetchobs(&dsid,1));

       %let rc=%sysfunc(close(&dsid));

     %put _user_;


    run;quit;

    *             _       _            _
      ___      __| | __ _| |_ __ _ ___| |_ ___ _ __
     / __|    / _` |/ _` | __/ _` / __| __/ _ \ '_ \
    | (__ _  | (_| | (_| | || (_| \__ \ ||  __/ |_) |
     \___(_)  \__,_|\__,_|\__\__,_|___/\__\___| .__/
                                              |_|
    ;
    * just in case the global variables and array  already exist - no relly needed;
    %symd el PCT_10 PCT_20 PCT_30 PCT_40 PCT_50 PCT_60 PCT_70 PCT_80 PCT_90;

    data _null_;
       set have;
       array vars _numeric_;
       do over vars;
          call symputx(vname(vars),vars);
       end;
    run;quit;

    %put _user_;


