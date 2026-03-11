from manim import *
import numpy as np

# ----------------------------------------------------
# ESCENA 1
# INTRODUCCIÓN DOCUMENTAL
# ----------------------------------------------------

class Intro(Scene):
    def construct(self):

        title = Text(
            "The Riemann Hypothesis",
            font_size=72
        )

        subtitle = Text(
            "A Harmonic Structure in the Complex Plane",
            font_size=40
        )

        subtitle.next_to(title,DOWN)

        self.play(FadeIn(title,shift=UP))
        self.play(Write(subtitle))

        self.wait(3)


# ----------------------------------------------------
# ESCENA 2
# DEFINICIÓN DE LA FUNCIÓN ZETA
# ----------------------------------------------------

class ZetaDefinition(Scene):
    def construct(self):

        eq = MathTex(
            r"\zeta(s)=\sum_{n=1}^{\infty}\frac{1}{n^s}"
        ).scale(1.5)

        self.play(Write(eq))

        sdef = MathTex(
            r"s=\sigma+it"
        )

        sdef.next_to(eq,DOWN)

        self.play(Write(sdef))

        self.wait(3)


# ----------------------------------------------------
# ESCENA 3
# PRODUCTO DE EULER
# ----------------------------------------------------

class EulerProduct(Scene):
    def construct(self):

        eq = MathTex(
            r"\zeta(s)=\prod_{p}\frac{1}{1-p^{-s}}"
        ).scale(1.5)

        text = Text(
            "Prime Number Structure",
            font_size=36
        )

        text.next_to(eq,DOWN)

        self.play(Write(eq))
        self.play(FadeIn(text))

        self.wait(3)


# ----------------------------------------------------
# ESCENA 4
# PLANO COMPLEJO
# ----------------------------------------------------

class ComplexPlaneScene(Scene):
    def construct(self):

        plane = ComplexPlane(
            x_range=[-2,2],
            y_range=[-30,30]
        )

        labels = plane.get_axis_labels(
            MathTex(r"\Re(s)"),
            MathTex(r"\Im(s)")
        )

        self.play(Create(plane))
        self.play(Write(labels))

        self.wait(3)


# ----------------------------------------------------
# ESCENA 5
# LÍNEA CRÍTICA
# ----------------------------------------------------

class CriticalLine(Scene):
    def construct(self):

        plane = ComplexPlane(
            x_range=[-2,2],
            y_range=[-30,30]
        )

        self.add(plane)

        line = Line(
            plane.c2p(0.5,-30),
            plane.c2p(0.5,30),
            color=YELLOW
        )

        label = MathTex(
            r"\Re(s)=\frac12"
        )

        label.next_to(line,RIGHT)

        self.play(Create(line))
        self.play(Write(label))

        self.wait(3)


# ----------------------------------------------------
# ESCENA 6
# REGIÓN CRÍTICA
# ----------------------------------------------------

class CriticalStrip(Scene):
    def construct(self):

        plane = ComplexPlane(
            x_range=[-1,2],
            y_range=[-30,30]
        )

        self.add(plane)

        strip = Rectangle(
            height=8,
            width=2,
            color=BLUE
        ).set_opacity(0.3)

        strip.move_to(plane.c2p(0.5,0))

        eq = MathTex(
            r"0<\Re(s)<1"
        )

        eq.to_edge(UP)

        self.play(FadeIn(strip))
        self.play(Write(eq))

        self.wait(3)


# ----------------------------------------------------
# ESCENA 7
# CEROS NO TRIVIALES
# ----------------------------------------------------

class RiemannZeros(Scene):
    def construct(self):

        plane = ComplexPlane(
            x_range=[0,1],
            y_range=[-40,40]
        )

        self.add(plane)

        zeros = [
            14.134725,
            21.022040,
            25.010857,
            30.424876,
            32.935061,
            37.586178,
            40.918719
        ]

        dots = VGroup()

        for z in zeros:

            dot = Dot(
                plane.c2p(0.5,z),
                color=RED
            )

            dots.add(dot)

        self.play(
            LaggedStart(
                *[FadeIn(d) for d in dots],
                lag_ratio=0.3
            )
        )

        self.wait(3)


# ----------------------------------------------------
# ESCENA 8
# SIMETRÍA
# ----------------------------------------------------

class Symmetry(Scene):
    def construct(self):

        plane = ComplexPlane()

        self.add(plane)

        y = 14.134725

        p1 = Dot(plane.c2p(0.5,y),color=BLUE)
        p2 = Dot(plane.c2p(0.5,-y),color=BLUE)

        line = Line(
            p1.get_center(),
            p2.get_center()
        )

        eq = MathTex(
            r"\rho \rightarrow 1-\rho"
        )

        eq.to_edge(DOWN)

        self.play(FadeIn(p1,p2))
        self.play(Create(line))
        self.play(Write(eq))

        self.wait(3)


# ----------------------------------------------------
# ESCENA 9
# ESTRUCTURA OSCILATORIA
# ----------------------------------------------------

class Oscillations(Scene):
    def construct(self):

        axes = Axes(
            x_range=[0,10],
            y_range=[-2,2]
        )

        graph = axes.plot(
            lambda x: np.cos(2*np.pi*x),
        )

        self.play(Create(axes))
        self.play(Create(graph))

        eq = MathTex(
            r"e^{-ix}+e^{ix}=2\cos(x)"
        )

        eq.to_edge(UP)

        self.play(Write(eq))

        self.wait(3)


# ----------------------------------------------------
# ESCENA 10
# ESTRUCTURA ARMÓNICA
# ----------------------------------------------------

class HarmonicStructure(Scene):
    def construct(self):

        eq = MathTex(
            r"\sum_{n=1}^{\infty} n^{-1/2}(e^{-ib\ln n}+e^{ib\ln n})"
        )

        self.play(Write(eq))

        box = SurroundingRectangle(eq)

        self.play(Create(box))

        self.wait(3)


# ----------------------------------------------------
# ESCENA 11
# PERTURBACIÓN
# ----------------------------------------------------

class Perturbation(Scene):
    def construct(self):

        eq = MathTex(
            r"s=q+ib"
        )

        cond = MathTex(
            r"q\neq\frac12"
        )

        cond.next_to(eq,DOWN)

        self.play(Write(eq))
        self.play(Write(cond))

        warn = Text(
            "Loss of harmonic balance",
            color=RED
        )

        warn.to_edge(DOWN)

        self.play(Write(warn))

        self.wait(3)


# ----------------------------------------------------
# ESCENA 12
# ESTABILIDAD
# ----------------------------------------------------

class Stability(Scene):
    def construct(self):

        eq = MathTex(
            r"n^{-1/2}+n^{-1/2}=2n^{-1/2}"
        )

        self.play(Write(eq))

        box = SurroundingRectangle(
            eq,
            color=GREEN
        )

        self.play(Create(box))

        self.wait(3)


# ----------------------------------------------------
# ESCENA 13
# INTERPRETACIÓN ESPECTRAL
# ----------------------------------------------------

class Spectral(Scene):
    def construct(self):

        eq = MathTex(
            r"\hat{H}\psi_n = \lambda_n \psi_n"
        )

        text = Text(
            "Spectral Interpretation",
            font_size=36
        )

        text.next_to(eq,DOWN)

        self.play(Write(eq))
        self.play(FadeIn(text))

        self.wait(3)


# ----------------------------------------------------
# ESCENA 14
# CONVERGENCIA
# ----------------------------------------------------

class Convergence(Scene):
    def construct(self):

        eq = MathTex(
            r"\lim_{t\to\infty} |\Re(\rho)-1/2| = 0"
        )

        self.play(Write(eq))

        self.wait(3)


# ----------------------------------------------------
# ESCENA 15
# CONCLUSIÓN
# ----------------------------------------------------

class Conclusion(Scene):
    def construct(self):

        eq = MathTex(
            r"\Re(s)=\frac12"
        ).scale(2)

        text = Text(
            "Critical Line Stability",
            font_size=40
        )

        text.next_to(eq,DOWN)

        self.play(Write(eq))
        self.play(Write(text))

        self.wait(4)
