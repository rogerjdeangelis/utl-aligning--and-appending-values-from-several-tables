# utl-aligning--and-appending-values-from-several-tables
Aligning and appending values from several tables
    Aligning and appending values from several tables                                                                                  
                                                                                                                                       
      Explanation                                                                                                                      
                                                                                                                                       
        Suppose you have two tables                                                                                                    
                                                                                                                                       
                   Table T1 | Table T2                                                                                                 
                            |                                                                                                          
                VAR  VAL    |  VAR VAL                                                                                                 
                            |                                                                                                          
                v0    A     |  v1   A                                                                                                  
                v0    C     |  v1   B                                                                                                  
                                                                                                                                       
        And you want (Transpose and align)                                                                                             
                                                                                                                                       
                 Table Want                                                                                                            
                            A   B  C                                                                                                   
                    V0      1   0  1    ** only A and C in column VAL in T1                                                            
                    V1      1   1  0                                                                                                   
                                                                                                                                       
    github                                                                                                                             
    https://tinyurl.com/y9d7ut26                                                                                                       
    https://github.com/rogerjdeangelis/utl-aligning--and-appending-values-from-several-tables                                          
                                                                                                                                       
    SAS Forum (related to)                                                                                                             
    https://tinyurl.com/y7e4bucz                                                                                                       
    https://communities.sas.com/t5/SAS-Programming/Creating-a-table-from-multiple-tables/m-p/665103                                    
                                                                                                                                       
    /*                   _                                                                                                             
    (_)_ __  _ __  _   _| |_                                                                                                           
    | | `_ \| `_ \| | | | __|                                                                                                          
    | | | | | |_) | |_| | |_                                                                                                           
    |_|_| |_| .__/ \__,_|\__|                                                                                                          
            |_|                                                                                                                        
    */                                                                                                                                 
    data T1;                                                                                                                           
    input val$ @@;                                                                                                                     
    var="v0";                                                                                                                          
    keep var val;                                                                                                                      
    cards4;                                                                                                                            
    A B C D E F G                                                                                                                      
    ;;;;                                                                                                                               
    run;quit;                                                                                                                          
                                                                                                                                       
    data T2;                                                                                                                           
    input Val$ @@;                                                                                                                     
    var="v1";                                                                                                                          
    keep var val;                                                                                                                      
    cards4;                                                                                                                            
    A B E G                                                                                                                            
    ;;;;                                                                                                                               
    run;                                                                                                                               
                                                                                                                                       
    data T3;                                                                                                                           
    input Val$ @@;                                                                                                                     
    var="v2";                                                                                                                          
    cards4;                                                                                                                            
    B C E F                                                                                                                            
    ;;;;                                                                                                                               
    run;quit;                                                                                                                          
                                                                                                                                       
    THREE TABLES                                                                                                                       
                                                                                                                                       
       Table T1 |  Table T2    | Table T3                                                                                              
                |              |                                                                                                       
    VAR  VAL    | VAR   VAL    | VAR   VAL                                                                                             
                |              |                                                                                                       
     v0   A     |  v1    A     |  v2    B                                                                                              
     v0   B     |  v1    B     |  v2    C                                                                                              
     v0   C     |  v1    E     |  v2    E                                                                                              
     v0   D     |  v1    G     |  v2    F                                                                                              
     v0   E                                                                                                                            
     v0   F                                                                                                                            
     v0   G                                                                                                                            
                                                                                                                                       
    /*           _               _                                                                                                     
      ___  _   _| |_ _ __  _   _| |_                                                                                                   
     / _ \| | | | __| `_ \| | | | __|                                                                                                  
    | (_) | |_| | |_| |_) | |_| | |_                                                                                                   
     \___/ \__,_|\__| .__/ \__,_|\__|                                                                                                  
                    |_|                                                                                                                
    */                                                                                                                                 
                                                                                                                                       
                                                                                                                                       
     WORK.WANT total obs=3                                                                                                             
                                                                                                                                       
      VAR    A    B    C    D    E    F    G                                                                                           
                                                                                                                                       
      v0     1    1    1    1    1    1    1  * Template                                                                               
                                                                                                                                       
      V1     1    1    0    0    1    0    1                                                                                           
      V2     0    1    1    0    1    1    0                                                                                           
                                                                                                                                       
                                                                                                                                       
    /*                                                                                                                                 
     _ __  _ __ ___   ___ ___  ___ ___                                                                                                 
    | `_ \| `__/ _ \ / __/ _ \/ __/ __|                                                                                                
    | |_) | | | (_) | (_|  __/\__ \__ \                                                                                                
    | .__/|_|  \___/ \___\___||___/___/                                                                                                
    |_|                                                                                                                                
    */                                                                                                                                 
                                                                                                                                       
    * create a key/val dictionary;                                                                                                     
    data havall;                                                                                                                       
       retain var;                                                                                                                     
       set t1 t2 t3;                                                                                                                   
    run;quit;                                                                                                                          
                                                                                                                                       
    /*                                                                                                                                 
    WORK.HAVALL total obs=15                                                                                                           
                                                                                                                                       
      VAR    VAL                                                                                                                       
                                                                                                                                       
      v0      A                                                                                                                        
      v0      B                                                                                                                        
      v0      C                                                                                                                        
      v0      D                                                                                                                        
      v0      E                                                                                                                        
      v0      F                                                                                                                        
      v0      G                                                                                                                        
                                                                                                                                       
      v1      A                                                                                                                        
      v1      B                                                                                                                        
      v1      E                                                                                                                        
      v1      G                                                                                                                        
                                                                                                                                       
      v2      B                                                                                                                        
      v2      C                                                                                                                        
      v2      E                                                                                                                        
      v2      F                                                                                                                        
    */                                                                                                                                 
                                                                                                                                       
    proc transpose data=havAll out=havXpo(drop=_name_);                                                                                
    by var notsorted;                                                                                                                  
    var val;                                                                                                                           
    id val;   ** important - this does the alignment;                                                                                  
    run;quit;                                                                                                                          
                                                                                                                                       
    /*                                                                                                                                 
    WORK.HAVXPO total obs=3                                                                                                            
                                                                                                                                       
      VAR    A    B    C    D    E    F    G                                                                                           
                                                                                                                                       
      v0     A    B    C    D    E    F    G   ** template record ;                                                                    
                                                                                                                                       
      v1     A    B              E         G                                                                                           
      v2          B    C         E    F                                                                                                
    */                                                                                                                                 
                                                                                                                                       
    * convert missing to 0 and populated to 1;                                                                                         
                                                                                                                                       
    %array(ns,values=%varlist(havXpo,keep=a--g));                                                                                      
                                                                                                                                       
    /* array creates these macro variables                                                                                             
    %put _user_;                                                                                                                       
                                                                                                                                       
    GLOBAL NSN 7                                                                                                                       
                                                                                                                                       
    GLOBAL NS1 A                                                                                                                       
    GLOBAL NS2 B                                                                                                                       
    GLOBAL NS3 C                                                                                                                       
    GLOBAL NS4 D                                                                                                                       
    GLOBAL NS5 E                                                                                                                       
    GLOBAL NS6 F                                                                                                                       
    GLOBAL NS7 G                                                                                                                       
    */                                                                                                                                 
                                                                                                                                       
    proc sql;                                                                                                                          
      create                                                                                                                           
         table want as                                                                                                                 
      select                                                                                                                           
        var                                                                                                                            
        /* cycle through the macro array above */                                                                                      
       ,%do_over(ns,phrase=case when missing(?) then 0 else 1 end as ?,between=comma)                                                  
      from                                                                                                                             
        havXpo                                                                                                                         
    ;quit;                                                                                                                             
                                                                                                                                       
                                                                                                                                       
    WORK.WANT total obs=3                                                                                                              
                                                                                                                                       
      VAR    A    B    C    D    E    F    G                                                                                           
                                                                                                                                       
      v0     1    1    1    1    1    1    1   * template ;                                                                            
                                                                                                                                       
      v1     1    1    0    0    1    0    1                                                                                           
      v2     0    1    1    0    1    1    0                                                                                           
                                                                                                                                       
                                                                                                                                       
                                                                                                                                       
