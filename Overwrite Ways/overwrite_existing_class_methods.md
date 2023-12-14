This overrides the method directly by setting the method on the class object. If this line is not called in a method, then the method will stay after the request is complete, so if there are other sites that don't have that app installed, they will be affected by the custom method behavior.

You can now override a standard DocType class via hooks.

for example you want to overwrite notification
test_app/hooks.py

override_doctype_class = {
	'ToDo': 'test_app.overrides.CustomToDo'
}

test_app/overrides.py

import frappe
from frappe.desk.doctype.todo.todo import ToDo


class CustomToDo(ToDo):
	def on_update(self):
		self.my_custom_code()
		super(ToDo, self).on_update()

	def my_custom_code(self):
		pass