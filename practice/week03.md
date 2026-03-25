import pygame import sys

초기화
pygame.init()

화면 설정
WIDTH, HEIGHT = 800, 600 screen = pygame.display.set_mode((WIDTH, HEIGHT)) pygame.display.set_caption("My First Pygame")

색상
WHITE = (255, 255, 255) BLACK = (0, 0, 0) BLUE = (0, 0, 255) RED = (255, 0, 0) GREEN = (0, 255, 0) YELLOW = (255, 255, 0) PURPLE = (160, 32, 240)

시계
clock = pygame.time.Clock()

폰트
font = pygame.font.SysFont(None, 30)

원 위치와 속도
circle_pos = [400, 300] speed = 5 circle_color = BLUE # 기본 색상

게임 루프
running = True while running: for event in pygame.event.get(): if event.type == pygame.QUIT: running = False

# 키 상태 확인
keys = pygame.key.get_pressed()

# Shift 키 확인
move_speed = speed * 2 if keys[pygame.K_LSHIFT] or keys[pygame.K_RSHIFT] else speed

# 방향키 움직임 + 색상 변경
if keys[pygame.K_LEFT]:
    circle_pos[0] -= move_speed
    circle_color = RED
elif keys[pygame.K_RIGHT]:
    circle_pos[0] += move_speed
    circle_color = GREEN
elif keys[pygame.K_UP]:
    circle_pos[1] -= move_speed
    circle_color = YELLOW
elif keys[pygame.K_DOWN]:
    circle_pos[1] += move_speed
    circle_color = PURPLE
else:
    circle_color = BLUE  # 키를 안 누르면 기본색

# 화면 채우기
screen.fill(WHITE)

# 원 그리기
pygame.draw.circle(screen, circle_color, circle_pos, 50)

# FPS 표시
fps = clock.get_fps()
fps_text = font.render(f"FPS: {fps:.2f}", True, BLACK)
screen.blit(fps_text, (10, 10))

# 화면 업데이트
pygame.display.flip()

# FPS 제한
clock.tick(60)
pygame.quit() sys.exit()
