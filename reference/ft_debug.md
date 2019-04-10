---
title: ft_debug
---
```
 FT_DEBUG prints a debug message on screen, depending on the verbosity 
 settings of the calling high-level FieldTrip function.

 Use as
   ft_debug(...)
 with arguments similar to fprintf, or
   ft_debug(msgId, ...)
 with arguments similar to warning.

 You can switch of all messages using
   ft_debug off
 or for specific ones using
   ft_debug off msgId

 To switch them back on, you would use 
   ft_debug on
 or for specific ones using
   ft_debug on msgId
 
 Messages are only printed once per timeout period using
   ft_debug timeout 60
   ft_debug once
 or for specific ones using
   ft_debug once msgId

 You can see the most recent messages and identifier using
   ft_debug last

 You can query the current on/off/once state for all messages using
   ft_debug query

 See also FT_ERROR, FT_WARNING, FT_NOTICE, FT_debug, FT_DEBUG, ERROR, WARNING
```
