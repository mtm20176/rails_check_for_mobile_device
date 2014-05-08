rails_check_for_mobile_device
=============================

Sometimes, you want to show view ERB specific to a device type.

Step 1
Add a helper in application controller:
```
  private

  # http://www.zytrax.com/tech/web/mobile_ids.html - for
  def mobile_device?
      request.user_agent =~ /Mobile/
  end
  helper_method :mobile_device?  
```

Step 2
call helper in view where you want to change ERB code.  In this case, the JS-powered pop-up is difficult to use on a tablet, so I revert to a standard form if mobile.
```
<% if mobile_device? %>

<%= link_to 'new', new_list_path  %>

<% else %>

<%= link_to_function 'new', 'loadPopupNew()',:id=>'popup_anchor', :tabindex=>'4' %>

<% end %>
```
