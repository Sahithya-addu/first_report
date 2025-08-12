# first_report
from PIL import Image
import numpy as np

def hide_image(cover_path, secret_path, output_path):
    # Load images
    cover_img = Image.open(cover_path).convert('RGB')
    secret_img = Image.open(secret_path).convert('RGB').resize(cover_img.size)

    # Convert to numpy arrays
    cover_arr = np.array(cover_img)
    secret_arr = np.array(secret_img)

    # Clear the last 4 bits of cover and store first 4 bits of secret
    stego_arr = (cover_arr & 0b11110000) | (secret_arr >> 4)

    # Save stego image
    stego_img = Image.fromarray(stego_arr.astype(np.uint8))
    stego_img.save(output_path)
    print(f"Secret image hidden successfully in {output_path}")

# Example usage
hide_image("cover.png", "secret.png", "stego.png")
