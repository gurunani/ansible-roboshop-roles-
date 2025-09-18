# RoboShop E-commerce - Ansible Setup

A simple e-commerce website deployed using Ansible automation.

## What's Inside

- **Frontend**: Nginx web server
- **Backend Services**: 
  - User service (NodeJS)
  - Cart service (NodeJS) 
  - Catalogue service (NodeJS)
  - Payment service (Python)
  - Shipping service (Java)
- **Databases**: MongoDB, MySQL, Redis
- **Message Queue**: RabbitMQ

## Quick Start

1. **Update your servers** in `inventory.ini`
2. **Run setup commands**:
   ```bash
   # Setup all services
   ansible-playbook -i inventory.ini main.yaml -e component=mongodb
   ansible-playbook -i inventory.ini main.yaml -e component=catalogue
   ansible-playbook -i inventory.ini main.yaml -e component=redis
   ansible-playbook -i inventory.ini main.yaml -e component=user
   ansible-playbook -i inventory.ini main.yaml -e component=cart
   ansible-playbook -i inventory.ini main.yaml -e component=mysql
   ansible-playbook -i inventory.ini main.yaml -e component=shipping
   ansible-playbook -i inventory.ini main.yaml -e component=rabbitmq
   ansible-playbook -i inventory.ini main.yaml -e component=payment
   ansible-playbook -i inventory.ini main.yaml -e component=frontend
   ```

## File Structure

```
├── inventory.ini          # Server details
├── main.yaml             # Main playbook
└── roles/
    ├── frontend/         # Nginx setup
    ├── user/            # User service
    ├── cart/            # Shopping cart
    ├── catalogue/       # Product catalog
    ├── payment/         # Payment processing
    ├── shipping/        # Shipping service
    ├── mongodb/         # Database
    ├── mysql/           # Database
    ├── redis/           # Cache
    ├── rabbitmq/        # Message queue
    └── common/          # Shared tasks
```

## Important Notes

- **Run in order**: Database services first, then backend services, then frontend
- **Check services**: `systemctl status service-name` 
- **View logs**: `journalctl -u service-name -f`
- **Test website**: Open your frontend server IP in browser

## Troubleshooting

- **Service not starting?** Check logs with `journalctl -u service-name`
- **Can't connect to database?** Verify database service is running
- **Order placement failing?** Check payment service logs

## Server Requirements

- RHEL/CentOS 9 or similar
- 2GB+ RAM per server
- Internet connection for package downloads