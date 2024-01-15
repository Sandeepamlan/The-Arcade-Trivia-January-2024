# Turn on Developer Mode
# select quiklabs_Ecommerce Project

# Create View - ```users_limited```
# Drag into Views Folder

```cmd 
views: users_limited {
sql_table_name: `cloud-training-demos.looker_ecomm.users` ;;

dimension: id {
  primary_key: yes
  type: number
  sql: ${TABLE}.id ;;
}

dimension: country {
  type: string
  map_layer_name: countries
  sql: ${TABLE}.country ;;
}

dimension: email {
  type: string
  sql: ${TABLE}.email ;;
}

dimension: first_name {
  type: string
  sql: ${TABLE}.first_name ;;
}

dimension: last_name {
  type: string
  sql: ${TABLE}.last_name ;;
}
measure: count {
  type: count
  drill_fields: [id, last_name, first_name]
}

}
```

# Save Changes and Click Validate LookML and then click Commit Changes & Push.

# Add a commit message and click Commit.

# Then click Deploy to Production.

# navigate to the training_ecommerce.model

```cmd
join: users_limited {
  type: left_outer
  sql_on: ${events.user_id} = ${users_limited.id};;
  relationship: many_to_one
}
```

# Save Changes and Click Validate LookML and then click Commit Changes & Push.

# Add a commit message and click Commit.

# Then click Deploy to Production.
