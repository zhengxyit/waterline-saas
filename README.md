# 增加了Sails 对SaaS（同库同表）的支持
# 1 sails config/models.js
> add config -> multitenant:true/false

# 2 modify waterline/core/index.js
> blew options(row 25)
```javascript
> this.multitenant = true;
      if (Object.getPrototypeOf(this).multitenant == false) {
          this.multitenant = false;
      }
```

> blew this._callbacks = schemaUtils.normalizeCallbacks(this);; add
```javascript
  // if multitenant==true add tenantId
  if(this.multitenant){
      this._attributes.tenantId = {type: 'text'};
  }
```

others look at commit