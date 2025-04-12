# frappe-custom-side-menu
Merubah Link yang ada di side menu Frappe Framework menjadi langsung ke view list DocType


script javascript
```
frappe.call({
    method: "frappe.client.get_list",
    args: {
      doctype: "Menu Replace",
      fields: ["target_link", "replace_with"],
    },
    callback: function (response) {
      if (response.message) {
        replaceMenuLink(response.message);
      } else {
        console.error("data found.");
      }
    },
    error: function (xhr, status, error) {
      console.error("Error fetching Menu Replace:", error);
    },
});

function replaceMenuLink(dataMenu) {
    dataMenu.forEach(function (t1) {
        $('.item-anchor').each(function(){
            var hreftarget = $(this).attr('href');
            if(hreftarget == t1.target_link ) $(this).attr('href',t1.replace_with);
        });
    });

}
```
