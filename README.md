# testing-consul-kv

testing consul_kv.py isolation.
I currently see two problems:  
* with my first pr can I be sure the behaviour does now not break for the usecase where no token is provided ? #2
* there are other params in the same categroy https://github.com/ansible-collections/community.general/pull/2126#discussion_r602850247 do we treat then as well 
 * #3 
 * see also next section as an attempt to understand this category of parameters.



## trying to understand the desired configuration state in the plugin

![image](images/config_state.svg)




##### plantuml of that
``` plantuml

@startuml
!include https://raw.githubusercontent.com/bschwarz/puml-themes/master/themes/spacelab/puml-theme-spacelab.puml

hide empty description
state config_free_parameters  {
config_free_parameters: **parameters** datacenter, index, port, recurse,scheme, token
config_free_parameters: **having defaults:** port, recurse, scheme 
config_free_parameters: **being optional:** datacenter, index, token
 

is_set: ..
has_default: ..
is_optional:..

[*]--> has_default
[*] --> is_optional

is_optional --> is_set
is_set--> [*] : yes: call with param
is_set--> [*] : no: call without param

has_default-->[*] : call with param

}
@enduml

``` 


