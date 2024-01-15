# Login to Looker
# Turn On Developer Mode
# Navigate back to the training_ecommerce.model file in the qwiklab_ecommerce project

```
conditionally_filter: {
filters: [created_date: "3 years"]
unless: [users.id, users.state]
}
```

# Click Validate LookML and then click Commit Changes & Push.

# Add a commit message and click Commit.

# click Deploy to Production.
