Experimenting with plugins using a shared library.

```
cd one && dune build @install && dune install && cd ..


cd two && dune build (* OK *)


(* Alternative builds *)

make (* Error *)

(*
File "./src/Two.v", line 2, characters 0-31:
Error:
Dynlink error: The module `Coq_config' is already loaded (either by the main program or a previously-dynlinked library)
*)

(* Clean up *)
make cleanall


(* Change the contents of two/src/Two.v to only 'Declare ML Module "two_plugin".' *)
dune build (* Error *)

(*
File "./src/Two.v", line 1, characters 0-31:
Error:
Dynlink error: error loading shared library: Dynlink.Error (Dynlink.Cannot_open_dll "Failure(\"/home/sam/code/coq/plugin-hell/two/_build/default/plugin/two_plugin.cmxs: undefined symbol: camlOne_plugin__Lib\")")
*)
```
