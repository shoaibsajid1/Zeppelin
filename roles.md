  roles:
    replaceDefaultOverrides: true #replaces default settings if true
    config:
      assignable_roles: #roles u can add to another user
        - '558037973581430785'
    overrides:
      - level: '>=50'
        config:
          can_assign: true #level 50 and up can assign
      - level: '>=100'
        config:
          can_mass_assign: true # level 100 can mass assign and remove roles
