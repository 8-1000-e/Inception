LOGIN	= edubois-

TPUT	= tput -T xterm-256color
_RESET	= $(shell $(TPUT) sgr0)
_GREEN	= $(shell $(TPUT) setaf 2)

all: up

up: 
	@mkdir -p /home/$(LOGIN)/data
	@mkdir -p /home/$(LOGIN)/data/mariadb
	@mkdir -p /home/$(LOGIN)/data/wordpress
	@export USER_ID=$$(id -u) && export GROUP_ID=$$(id -g) && docker compose -f ./srcs/docker-compose.yml up -d

down:
	@printf "\n🔧 $(_GREEN)Down containers$(_RESET) 🔧\n\n"
	@docker compose -f ./srcs/docker-compose.yml down --volumes

logs:
	@printf "\n📋 $(_GREEN)Show containers logs$(_RESET) 📋\n\n"
	@docker compose -f ./srcs/docker-compose.yml logs -f

clean: down
	@printf "\n🔧 $(_GREEN)Delete /home/$(LOGIN)/data$(_RESET) 🔧\n\n"
	@docker volume rm -f mariadb wordpress 2>/dev/null || true
	@rm -rf /home/$(LOGIN)/data 2>/dev/null || true

fclean: clean
	@printf "\n🔧 $(_GREEN)Delete containers images$(_RESET) 🔧\n\n"
	@docker system prune -af

re: fclean all

.PHONY:
	all up down logs clean fclean re
