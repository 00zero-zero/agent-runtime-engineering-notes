# Discovery versus admission

Resource discovery describes what is available. Admission decides whether available resources satisfy a frozen run specification.

Discovery may report models, tools, accelerators, environments, versions, health, and capacity. It must not decide that a weaker substitute is close enough.

Admission consumes those facts together with compiled requirements and either produces an explicit binding or fails closed. Record the selected binding as run evidence.

Keeping these stages separate prevents operational inventory code from redefining scientific semantics.
