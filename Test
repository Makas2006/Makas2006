import requests
from colorama import init, Fore, Back
from pyfiglet import Figlet
from PIL import Image, ImageDraw, ImageChops
from random import randint, random
import colorsys

init(autoreset=True)


def getcolor():
  h = random()
  s = 1
  v = 1

  float_rgb = colorsys.hsv_to_rgb(h, s, v)
  rgb = [int(x * 255) for x in float_rgb]

  return tuple(rgb)


def interpole(start_color, end_color, factor: float):
  recip = 1 - factor
  return (
    int(start_color[0] * recip + end_color[0] * factor),
    int(start_color[1] * recip + end_color[1] * factor),
    int(start_color[2] * recip + end_color[2] * factor)
  )


def render(text, style):
  """Render preview"""
  f = Figlet(font=style)
  print(f'{Back.WHITE}{Fore.BLACK}By IceForge(TeleGram) - @ice_forge')
  print('\n')
  print(Fore.GREEN + f.renderText(text))


def generate_art(filename):
  """Generating Art"""
  print('Generating art...')
  target_size_px = 256
  scale_factor = 2
  start_color = getcolor()
  end_color = getcolor()

  size_px = target_size_px * scale_factor
  bg_color = (0, 0, 0)
  padding_px = 16 * scale_factor

  image = Image.new(
          "RGB", 
          (size_px, size_px), 
          bg_color)

  # Draw on image
  draw = ImageDraw.Draw(image)
  points = []

  for i in range(15):
    line_point = (randint(padding_px, size_px - padding_px), randint(padding_px, size_px - padding_px))
    points.append(line_point)

  thickness = 1
  n_points = len(points) - 1
  for i, point in enumerate(points):
    # overlay canvas
    overlay = Image.new(
          "RGB", 
          (size_px, size_px), 
          bg_color)
    overlay_draw = ImageDraw.Draw(overlay)

    p1 = point

    if i == n_points:
      p2 = points[0]
    else:
      p2 = points[i + 1]

    line_xy = (p1, p2)
    color_factor = i / n_points
    line_color = interpole(start_color, end_color, color_factor)
    thickness += scale_factor
    overlay_draw.line(line_xy, fill=line_color, width=thickness)
    image = ImageChops.add(image, overlay)

  # Save image
  image = image.resize((target_size_px, target_size_px), resample=Image.ANTIALIAS)
  image.save(filename)

  print(f'NFT is generate! File: {filename}')


if __name__ == '__main__':
  render('Creator\nNFT', 'banner3-D')
  for i in range(int(input('Enter count NFT: '))):
    generate_art(f'nft_{i}.png')
