# React + Vite

This template provides a minimal setup to get React working in Vite with HMR and some ESLint rules.

Currently, two official plugins are available:

- [@vitejs/plugin-react](https://github.com/vitejs/vite-plugin-react/blob/main/packages/plugin-react/README.md) uses [Babel](https://babeljs.io/) for Fast Refresh
- [@vitejs/plugin-react-swc](https://github.com/vitejs/vite-plugin-react-swc) uses [SWC](https://swc.rs/) for Fast Refresh

```mermaid
erDiagram
    users {
        id integer PK
        email character_varying(255)
        password_hash text
        stripe_customer_id character_varying(255)
        created_at timestamp
        updated_at timestamp
    }

    user_details {
        id integer PK
        user_id integer FK
        full_name character_varying(255)
        avatar_url text
        username character_varying(255)
        date_of_birth date
        weight integer
        height integer
        gender gender_enum
        created_at timestamp
        updated_at timestamp
    }

    user_achievements {
        id integer PK
        user_id integer FK
        achievement_id integer FK
        created_at timestamp
        updated_at timestamp
    }

    achievements {
        id integer PK
        name character_varying(255)
        activity_type activity_type_enum
        requirement integer
        requirement_metric requirement_metric_enum
        created_at timestamp
        updated_at timestamp
    }

    subscriptions {
        id integer PK
        user_id integer FK
        plan_id integer FK
        stripe_subscription_id character_varying(255)
        is_canceled boolean
        expires_at timestamp
        created_at timestamp
        updated_at timestamp
        status status_enum
    }

    subscription_plans {
        id integer PK
        name character_varying(255)
        price numeric(8-2)
        description text
        stripe_product_id character_varying(255)
        stripe_price_id character_varying(255)
        created_at timestamp
        updated_at timestamp
    }

    oauth_info {
        id integer PK
        user_id integer FK
        token_type character_varying(255)
        expires_at bigint
        access_token text
        refresh_token text
        scope character_varying(255)
        provider oauth_provider_enum
        created_at timestamp
        updated_at timestamp
    }

    goals {
        id integer PK
        user_id integer FK
        frequency integer
        frequency_type frequency_type_enum
        distance real
        duration integer
        progress real
        completed_at timestamp
        created_at timestamp
        updated_at timestamp
    }

    oauth_state {
        id integer PK
        user_id integer FK
        uuid character_varying(255)
        created_at timestamp
        updated_at timestamp
    }

    users ||--o{ user_details : user_id
    users ||--o{ user_achievements : user_id
    achievements ||--o{ user_achievements : achievement_id
    users ||--o{ subscriptions : user_id
    subscription_plans ||--o{ subscriptions : plan_id
    users ||--o{ oauth_info : user_id
    users ||--o{ goals : user_id
    users ||--o{ oauth_state : user_id
```
