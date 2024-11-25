# Local Privilage Escalation Cheatsheet
Tags: #template 
Related to: #note-taking, #notes
See also: 
Index: [[🗂️ Index of CRTP]]

#### Service Issues using PowerUp
| Function                                                                                           | Command                               |
| -------------------------------------------------------------------------------------------------- | ------------------------------------- |
| Get services with unquoted paths and a space in their name                                         | `Get-ServiceUnquoted -Verbose`        |
| Get services where the current user can write to its binary path or change arguments to the binary | `Get-ModifiableServiceFile -Versbose` |
| Get services whose configuration can be modified by current user                                                                                                 | `Get-ModifiableService -Versbose`                                      |

#### Run all checks using tools 
| Tool    | Command for running all checks |
| ------- | ------------------------------ |
| PowerUp | `Invoke-AllChecks`             |
| BeRoot  | `.\beRoot.exe`                 |
| Privesc | `Invoke-PrivEsc`               |
