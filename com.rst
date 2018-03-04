Specification for Server to Client Communication
================================================

*version 2018/03/04*

NOTE: This document is subjected to change, modifications can and will happen
until a final release is available.

The purpose of this document is to inform what available commands you can send
to the server for each client. This document is divided into two section, first
the client to server communication and next server to client. Each section will
be divided into available commands and responses.

Available Commands
------------------

Client to Server
^^^^^^^^^^^^^^^^

The client is sending to the server a UTF-8 string with the following
format: ::

   { 'version': '0.2', 'type': <string>, 'value': ...  }


Where `version` is the protocol version number, `type` the type of
command, and the `value` the corresponding value which the command
should handle (see the description below).

The following commands should be available (not in a particular order): ::

   get_board

   get_active_block
   move_active_block

   get_queued_powerup
   use_queued_powerup

   set_name

   start_game
   end_game


The server will answer in this format: ::

   { 'version': '0.2',
     'response_type': <string>,
     'value': ...
   }


Their corresponding values are:

get_board
"""""""""
Send: ::

   ...
   'value': <boolean> }

Response: ::

   { 'version': '0.2',
     'response_type': 'board',
     'value': <int_array>
   }


get_active_block
""""""""""""""""
Send: ::

   ...
   'value': <boolean>}

Response: ::

   { 'version': '0.2',
     'response_type': 'active_block',
     'value': <string>
   }

where `<string>` can be one of these: ::

   L-block
   RevL-block
   I-block
   Z-block
   RevZ-block
   T-block
   S-block

move_active_block
"""""""""""""""""
Send: ::

   ...
   'value': <string> }

where the string is either `left`, `right`, `down`, `rotate` or `hard_drop`.

Response: ::

   { 'version': '0.2',
     'response_type': 'status',
     'value': <int>
   }

1 for ok, or 0 for error.

get_queued_powerup
""""""""""""""""""
Send: ::

   ...
   'value': <boolean>}

Response: ::

   { 'version': '0.2',
     'response_type': 'queued_powerup',
     'value': <string>
   }

where `<string>` can be one of these: ::

   AddRow
   Earthquake
   Milkshake
   Specialgone
   Shotgun
   Gravity
   ClearBoard
   SwitchBoard
   
use_queued_powerup
""""""""""""""""""
Send: ::

   ...
   'value': <boolean>}

Response: ::

   { 'version': '0.2',
     'response_type': 'board',
     'value': <int_array>
   }

set_name
""""""""
Send: ::

   ...
   'value': <string> }

Response: ::

   { 'version': '0.2',
     'response_type': 'status',
     'value': <int>
   }

1 for ok, or 0 for error.

start_game
""""""""""

Send: ::

   ...
   'value': <boolean> }

Response: ::

   { 'version': '0.2',
     'response_type': 'status',
     'value': <int>
   }

1 for ok, or 0 for error.

end_game
""""""""

Send: ::

   ...
   'value': <boolean> }

Response: ::

   { 'version': '0.2',
    'response_type': 'status',
    'value': <int>
   }

1 for ok, or 0 for error 
