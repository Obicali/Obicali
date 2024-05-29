-@startuml
skinparam ActivityBackgroundColor #FFFFCC
skinparam ActivityBorderColor #FF9900
skinparam ActivityDiamondBackgroundColor #FFCCCC
skinparam ActivityDiamondBorderColor #FF0000
skinparam NoteBackgroundColor #CCFFCC
skinparam NoteBorderColor #009900

title Tool Management Application Flow

start

:User Login;

if (Valid User?) then (Yes)
  :Display Main Menu;

  if (Option Selected?) then (Tool Inventory)
    :Manage Tool Inventory;
    note right
      - View Inventory
      - Add/Update/Remove Tools
      - Set Minimum Stock Levels
    end note

  elseif (Option Selected?) then (Borrow Tools)
    :Browse Tool Inventory;
    :Request Tool Borrowing;
    if (Approval Required?) then (Yes)
      :Notify Tool Manager;
      if (Approved?) then (Yes)
        :Update Tool Inventory;
        :Generate Borrowing Record;
      else (No)
        :Reject Borrowing Request;
      endif
    else (No)
      :Update Tool Inventory;
      :Generate Borrowing Record;
    endif

  elseif (Option Selected?) then (Return Tools)
    :Browse Borrowed Tools;
    :Mark Tools as Returned;
    :Update Tool Inventory;
    if (Damage Reported?) then (Yes)
      :Raise Damage Report;
    endif

  elseif (Option Selected?) then (Reports)
    :Filter Reports;
    note right
      - Tool Usage
      - Borrowing History
      - Inventory Levels
    end note
    :Generate Reports;

  else (Logout)
    :Logout;
  endif

else (No)
  :Display Login Error;
endif

stop

@enduml
