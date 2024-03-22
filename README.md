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
        created_at timestamp
        updated_at timestamp
        stripe_customer_id character_varying(255)
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
        referral_code character_varying(255)
        bonus_balance integer
        location character_varying(255)
        is_public boolean
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

    user_achievements {
        id integer PK
        user_id integer FK
        achievement_id integer FK
        created_at timestamp
        updated_at timestamp
    }

    schedules {
        id integer PK
        user_id integer FK
        goal_id integer FK
        start_at timestamp
        activity_type activity_type_enum
        created_at timestamp
        updated_at timestamp
    }

    goals {
        id integer PK
        user_id integer FK
        activity_type activity_type_enum
        frequency integer
        frequency_type frequency_type_enum
        distance real
        duration integer
        progress real
        completed_at timestamp
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
        status status_enum
        created_at timestamp
        updated_at timestamp
    }

    subscription_plans {
        id integer PK
        name character_varying(255)
        price numeric(8_2)
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
        owner_id integer
    }

    workouts {
        id integer PK
        user_id integer FK
        steps real
        activity_id character_varying(255)
        kilocalories real
        heart_rate real
        workout_started_at timestamp
        workout_ended_at timestamp
        distance real
        speed real
        activity_type activity_type_enum
        created_at timestamp
        updated_at timestamp
        provider oauth_provider_enum
    }

    notifications {
        id integer PK
        user_id integer FK
        title character_varying(255)
        message character_varying(255)
        is_read boolean
        type notification_type_enum
        created_at timestamp
        updated_at timestamp
    }

    user_bonuses {
        id integer PK
        user_id integer FK
        amount integer
        created_at timestamp
        updated_at timestamp
        action_type action_type_enum
        transaction_type transaction_type_enum
    }

    oauth_state {
        id integer PK
        user_id integer FK
        uuid character_varying(255)
        created_at timestamp
        updated_at timestamp
        referral_code character_varying(255)
    }

    messages {
        id integer PK
        chat_id integer FK
        sender_id integer FK
        text text
        is_seen boolean
        created_at timestamp
        updated_at timestamp
    }

    chats {
        id integer PK
        is_assistant boolean
        created_at timestamp
        updated_at timestamp
    }

    chats_users {
        id integer PK
        chat_id integer FK
        user_id integer FK
        created_at timestamp
        updated_at timestamp
    }

    friends {
        id integer PK
        user_id integer FK
        following_id integer FK
        created_at timestamp
        updated_at timestamp
    }

    users ||--o{ user_details : user_id
    users ||--o{ user_achievements : user_id
    achievements ||--o{ user_achievements : achievement_id
    users ||--o{ schedules : user_id
    goals ||--o{ schedules : goal_id
    users ||--o{ goals : user_id
    users ||--o{ subscriptions : user_id
    subscription_plans ||--o{ subscriptions : plan_id
    users ||--o{ oauth_info : user_id
    users ||--o{ workouts : user_id
    users ||--o{ notifications : user_id
    users ||--o{ user_bonuses : user_id
    users ||--o{ oauth_state : user_id
    users ||--o{ messages : sender_id
    users ||--o{ friends : user_id
    users ||--o{ friends : following_id
    chats ||--o{ chats_users : chat_id
    users ||--o{ chats_users : user_id
    friends ||--o{ chats : id
    friends ||--o{ messages : chat_id
```
