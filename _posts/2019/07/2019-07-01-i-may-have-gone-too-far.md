---
layout: post
title: "I May Have Gone Too Far"
date: 2019-07-01
tags: [ personal, supercollider ]
---

Given that every single {% include tag_link.html tag="supercollider" %} oscillator that I've studied so far uses a
purely linear expansion on the differential equation it is probably overbuilding in the extreme that I've settled on
a 6th order RKNG integration algorithm with *eight function evaluations* per step. I spent a considerable amount of time
this evening, after a lot of head scratching, in just typing out the parameters for the algorithm. I'm working on an
implementation of the algorithm detailed in "Sharp, P.W. and J.M. Fine, Some Nystrom pairs for the general second-order
initial-value problem, Journal of Computational and Applied Mathematics 42 (1992) 279-291." This is what I have
so far:

```
template<typename ODE>
void SharpFineRKNG8(const ODE& f, const double h, const double x, const double y, const double yPrime,
    const double yHat, const double yPrimeHat, double& yOut, double& yPrimeOut, double& yHatOut, double& yPrimeHatOut) {
    constexpr double c_1 = 1.0;
    constexpr double c_2 = 1.0 / 10.0;
    constexpr double c_3 = 2.0 / 9.0;
    constexpr double c_4 = 3.0 / 7.0;
    constexpr double c_5 = 2.0 / 3.0;
    constexpr double c_6 = 4.0 / 5.0;
    constexpr double c_7 = 1.0;
    constexpr double c_8 = 1.0;

    constexpr double b_1 = 23.0 / 320.0;
    constexpr double b_2 = 0.0;
    constexpr double b_3 = 12393.0 / 54080.0;
    constexpr double b_4 = 2401.0 / 25350.0;
    constexpr double b_5 = 99.0 / 1600.0;
    constexpr double b_6 = 1375.0 / 32448.0;
    constexpr double b_7 = 0.0;
    constexpr double b_8 = 0.0;

    // TODO: bPrimes, bHats!

    constexpr double a_21 = 1.0 / 200.0;

    constexpr double a_31 = 14.0 / 2187.0;
    constexpr double a_32 = 40.0 / 2187.0;

    constexpr double a_41 = 148.0 / 3087.0;
    constexpr double a_42 = -85.0 / 3087.0;
    constexpr double a_43 = 1.0 / 14.0;

    constexpr double a_51 = -2201.0 / 28350.0;
    constexpr double a_52 = 932.0 / 2835.0;
    constexpr double a_53 = -7.0 / 50.0;
    constexpr double a_54 = 1.0 / 9.0;

    constexpr double a_61 = 13198826.0 / 54140625.0;
    constexpr double a_62 = -5602364.0 / 10828215.0;
    constexpr double a_63 = 278987101.0 / 44687500.0;
    constexpr double a_64 = -332539.0 / 4021872.0;
    constexpr double a_65 = 1.0 / 20.0;

    constexpr double a_71 = -601416947.0 / 16216200.0;
    constexpr double a_72 = 2972539.0 / 810810.0;
    constexpr double a_73 = 10883471.0 / 2574000.0;
    constexpr double a_74 = -503477.0 / 99000.0;
    constexpr double a_75 = 3.0 / 5.0;
    constexpr double a_76 = 4.0 / 5.0;

    constexpr double a_81 = -228527046421.0 / 72442188000.0;
    constexpr double a_82 = 445808287.0 / 139311900.0;
    constexpr double a_83 = 104724572891.0 / 29896776000.0;
    constexpr double a_84 = -31680158501.0 / 747419400.0;
    constexpr double a_85 = 1033813.0 / 2044224.0;
    constexpr double a_86 = 1166143.0 / 1703520.0;
    constexpr double a_87 = 0.0;

    // TODO: aPrimes!

    double f_1 = f(x + (h * c_1), y + (h * c_1 * yPrime), yPrime);
    double f_2 = f(x + (h * c_2), y + (h * c_2 * yPrime) + (h * h * (a_21 * f_1)), yPrime + (h * (aPrime_21 * f1)));
    double f_3 = f(x + (h * c_3), y + (h * c_3 * yPrime) + (h * h * ((a_31 * f_1) + (a_32 * f_2))), yPrime + (h *
        ((aPrime_31 * f_1) + (aPrime_32 * f_2))));
    double f_4 = f(x + (h * c_4), y + (h * c_4 * yPrime) + (h * h * ((a_41 * f_1) + (a_42 * f_2) + (a_43 * f_3))),
        yPrime + (h * ((aPrime_41 * f_1) + (aPrime_42 * f_2) + (aPrime_43 * f_3))));
    double f_5 = f(x + (h * c_5), y + (h * c_5 * yPrime) + (h * h * ((a_51 * f_1) + (a_52 * f_2) + (a_53 * f_3) + (a_54
        * f_4))), yPrime + (h * ((aPrime_51 * f_1) + (aPrime_52 * f_2) + (aPrime_53 * f3) + (aPrime_54 * f4))));
    double f_6 = f(x + (h * c_6), y + (h * c_6 * yPrime) + (h * h * ((a_61 * f_1) + (a_62 * f_2) + (a_63 * f_3) + (a_64
        * f_4) + (a_65 * f_5))), yPrime + (h * ((aPrime_61 * f_1) + (aPrime_62 * f_2) + (aPrime_63 * f_3) + (aPrime_64 *
        f_4) + (aPrime_65 * f_5))));
    double f_7 = f(x + (h * c_7), y + (h * c_7 * yPrime) + (h * h * ((a_71 * f_1) + (a_72 * f_2) + (a_73 * f_3) + (a_74
        * f_4) + (a_75 * f_5) + (a_76 * f_6))), yPrime + (h * ((aPrime_71 * f_1) + (aPrime_72 * f_2) + (aPrime_73 * f_3)
        + (aPrime_74 * f_4) + (aPrime_75 * f_5) + (aPrime_76 * f_6))));
    double f_8 = f(x + (h * c_8), y + (h * c_8 * yPrime) + (h * h * ((a_81 * f_1) + (a_82 * f_2) + (a_83 * f_3) + (a_84
        * f_4) + (a_85 * f_5) + (a_86 * f_6) + (a_87 * f_7))), yPrime + (h * ((aPrime_81 * f_1) + (aPrime_82 * f_2) +
        (aPrime_83 * f_3) + (aPrime_84 * f_4) + (aPrime_85 * f_5) + (aPrime_86 * f_6) + (aPrime_87 * f_7))));
}
```

which is straight-up crazytown! Actually figuring this out was a bunch of fun. But once I got in to typing the function
evals ```f1``` through ```f8``` I knew I was going to have to type them all out or lose the pattern and have to start
all over. I think the plan now is to try and find some closed-form second-order differential equations and compare the
integration step with the closed solution, or maybe get some Matlab going to test their integrator against mine. Then
there's a build system and other fun challenges to get this thing plugged in to SuperCollider and generating audio
signals. There's also, of course, always the distinct possibility that this is way overcomplicated and will not be able
to fill a single buffer suitable for realtime audio. Like, there's probably a pretty good reason that the other chaotic
oscillator implementations I'm seeing only do the linear approximation. But I also notice that they are full of
instability detections, including checks for values blowing up as well as NAN (not a number) detection. So I am a bit
curious if I'll be able to spend the extra compute in order for a great increase in stability. And if not, oh well, it's
been fun flexing my (very out of shape) math muscles!

