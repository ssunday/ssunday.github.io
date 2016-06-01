---
layout: post
title: Acquiring a Mild Command Over Command Patterns
description: Turning a menu into a bunch of objects
date: 25/2/2016
---
Instead of having a menu for an app be a set of if/else or case statements, one can make it using a variety objects. This style is known as the ‘Command Pattern.’ Basically, the menu turns into a group of classes that each have the particular command or execution method that is called by the core menu class.

It was decided that I should implement this with my Time Logger App, where originally I had a if/else block testing the user defined option selection and then performing the command that was a function in the file. With using the command pattern, I have a class that has a hash map of option selections and the respective object that acts as their execution.

```ruby
class TimeLoggerMenu

  MENU_OPTIONS_EMPLOYEE = {1 => TimeLoggerLogHoursMenuOption.new,
                  2 => TimeLoggerEmployeeReportTimeOption.new,
                  3 => TimeLoggerLogoutOption.new}


  MENU_OPTIONS_ADMIN = {1 => TimeLoggerLogHoursMenuOption.new,
                  2 => TimeLoggerEmployeeReportTimeOption.new,
                  3 => TimeLoggerCurrentMonthReportOption.new,
                  4 => TimeLoggerAddEmployeeOption.new ,
                  5 => TimeLoggerAddClientOption.new,
                  6 => TimeLoggerLogoutOption.new}

  def initialize(logger, io)
    @data_logger = logger
    @io = io
  end

  def assign_menu_based_on_whether_employee_is_admin(is_user_admin)
    @active_menu = is_user_admin ? MENU_OPTIONS_ADMIN : MENU_OPTIONS_EMPLOYEE
  end

  def do_menu_option(option, username)
    if @active_menu[option] == nil
      @io.invalid_option_message
    else
      @active_menu[option].execute(@data_logger, @io, username)
    end
  end

  def options
    @active_menu.values.map {|option| option.to_s}
  end

end
```

The do_menu_option calls the execute function of the classes, which all of them have as they inherit from a menu_option superclass. Execute performs the particular option that the user selected. The code to perform that function is present with that class and relevant modules.

I implemented this with my app and it reduced the file sizes of the app file by over half. It cut down on duplication and made it much more readable. It also made testing much easier, as each separate option was now testable. It really modularized the entire app. Another upside is that if I were to add another option to either the employee or admin menus, it would be much simpler and wouldn’t change the app or most of the app_menu code. I would create another class and then add it to the hashmap.

[The code in full can be explored here.](https://github.com/ssunday/TimeLoggerApp)

I was hesitant about the Command Pattern style at first—it seemed a bit over-the-top, but getting into it and experiencing it, I really see the positive effects from it.
