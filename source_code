from PyQt6.QtWidgets import QApplication, QLabel
from PyQt6.QtGui import QPixmap, QImage
from PyQt6.QtCore import Qt, QTimer, QPoint
from PIL import Image
import sys
import os

# Path to GIF, add full path to your gif and keep the quotes
gif_path = ""
if not os.path.exists(gif_path):
    print("GIF not found at:", gif_path)
    sys.exit(1)

app = QApplication(sys.argv)

# Fixed scale factor to reduce size by 60%, size can be changed here
scale_factor = 0.4

# Load GIF frames with PIL and convert to QImage
im = Image.open(gif_path)
frames = []
delays = []
try:
    while True:
        frame = im.convert("RGBA")
        data = frame.tobytes("raw", "RGBA")
        qimage = QImage(data, frame.width, frame.height,
                        QImage.Format.Format_RGBA8888)
        frames.append(qimage.copy())
        delays.append(im.info.get("duration", 100))
        im.seek(im.tell() + 1)
except EOFError:
    pass

frame_count = len(frames)
current_frame = 0

# QLabel for sprite
label = QLabel()
label.setWindowFlags(
    Qt.WindowType.FramelessWindowHint |
    Qt.WindowType.WindowStaysOnTopHint |
    Qt.WindowType.Tool
)
label.setAttribute(Qt.WidgetAttribute.WA_TranslucentBackground)

# Dragging
drag_pos = QPoint()


def mousePressEvent(event):
    global drag_pos
    if event.button() == Qt.MouseButton.LeftButton:
        drag_pos = event.globalPosition().toPoint() - label.pos()


def mouseMoveEvent(event):
    if event.buttons() & Qt.MouseButton.LeftButton:
        label.move(event.globalPosition().toPoint() - drag_pos)


def keyPressEvent(event):
    if event.key() == Qt.Key.Key_Escape:
        app.quit()
    elif event.key() == Qt.Key.Key_F1:
        label.setVisible(not label.isVisible())


label.mousePressEvent = mousePressEvent
label.mouseMoveEvent = mouseMoveEvent
label.keyPressEvent = keyPressEvent


def render_current_frame():
    qimage = frames[current_frame]
    pixmap = QPixmap.fromImage(qimage)
    scaled_pixmap = pixmap.scaled(
        int(pixmap.width() * scale_factor),
        int(pixmap.height() * scale_factor),
        Qt.AspectRatioMode.KeepAspectRatio,
        Qt.TransformationMode.SmoothTransformation
    )
    label.setPixmap(scaled_pixmap)
    label.resize(scaled_pixmap.size())


def advance_frame():
    global current_frame
    render_current_frame()
    current_frame = (current_frame + 1) % frame_count
    QTimer.singleShot(delays[current_frame], advance_frame)


# Start animation
advance_frame()
label.move(300, 300)
label.show()

sys.exit(app.exec())
