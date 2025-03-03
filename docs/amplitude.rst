----------------
Amplitude
----------------


Helicity Formula
________________

Each Decay has Amplitude defined like:

.. math::
    A^{A \rightarrow B+C}_{\lambda_{A},\lambda_{B},\lambda_{C}} = H_{\lambda_{B},\lambda_{C}}^{A \rightarrow B+C} D^{J_{A}\star}_{\lambda_{A},\lambda_{B}-\lambda_{C}}(\phi,\theta,0)

For a chain decay, amplitude can be combined as

.. math::
    A^{A \rightarrow R+B,R \rightarrow C+D}_{\lambda_{A},\lambda_{B},\lambda_{C},\lambda_{D}}
    = \sum_{\lambda_{R}}A^{A \rightarrow R+B}_{\lambda_{A},\lambda_{R},\lambda_{B}}
    \color{red}{R(m_{R})}\color{black} A^{R \rightarrow C+D} _{\lambda_{R},\lambda_{C},\lambda_{D}}

with angle aligned

.. math::
    {\hat{A}}^{A \rightarrow R+B,R \rightarrow C+D}_{\lambda_{A},\lambda_{B},\lambda_{C},\lambda_{D}}
    = \sum_{\lambda_{B}',\lambda_{C}',\lambda_{D}'}A^{A \rightarrow R+B,R \rightarrow C+D}_{\lambda_{A},\lambda_{B}',\lambda_{C}',\lambda_{D}'}
    D^{J_{B}\star}_{\lambda_{B}',\lambda_{B}}(\alpha_{B},\beta_{B},\gamma_{B})
    D^{J_{C}\star}_{\lambda_{C}',\lambda_{C}}(\alpha_{C},\beta_{C},\gamma_{C})
    D^{J_{D}\star}_{\lambda_{D}',\lambda_{D}}(\alpha_{D},\beta_{D},\gamma_{D})

the sum of resonances

.. math::
    A_{\lambda_{A},\lambda_{B},\lambda_{C},\lambda_{D}}^{total} = \sum_{R_{1}} {\hat{A}}^{A \rightarrow R_{1}+B,R_{1} \rightarrow C+D}_{\lambda_{A},\lambda_{B},\lambda_{C},\lambda_{D}}
    + \sum_{R_{2}} {\hat{A}}^{A \rightarrow R_{2}+C,R_{2} \rightarrow B+D}_{\lambda_{A},\lambda_{B},\lambda_{C},\lambda_{D}}
    + \sum_{R_{3}} {\hat{A}}^{A \rightarrow R_{3}+D,R_{3} \rightarrow B+C}_{\lambda_{A},\lambda_{B},\lambda_{C},\lambda_{D}}


then the differential cross-section

.. math::
    \frac{\mathrm{d}\sigma}{\mathrm{d}\Phi} = \frac{1}{N}\sum_{\lambda_{A}}\sum_{\lambda_{B},\lambda_{C},\lambda_{D}}|A_{\lambda_{A},\lambda_{B},\lambda_{C},\lambda_{D}}^{total}|^2



Amplitude Combination Rules
---------------------------

For a decay process :code:`A -> R B, R -> C D`, we can get different part of amplitude:

1. Particle:
    1. Initial state: :math:`1`

    2. Final state: :math:`D(\alpha, \beta, \gamma)`

    3. Propagator: :math:`R(m)`

2. Decay:
    Two body decay (:code:`A -> R B`): :math:`H_{\lambda_R,\lambda_B} D_{\lambda_A, \lambda_R - \lambda_B} (\varphi, \theta,0)`

Now we can use combination rules to build amplitude for the whole process.

    Probability Density:
        :math:`P = |\tilde{A}|^2` (modular square)

        Decay Group:
            :math:`\tilde{A} = a_1 A_{R_1} + a_2 A_{R_2} + \cdots` (addition)

            Decay Chain:
                :math:`A_{R} = A_1 \times R \times A_2 \cdots` (multiplication)

                Decay:
                :math:`A_i = HD(\varphi, \theta, 0)`

                Particle:
                :math:`R(m)`

The indices part is quantum number, and it can be summed automatically.



Default Amplitude Model
------------------------

The defalut model for Decay is helicity amplitude

.. math::
   A^{A \rightarrow B C}_{\lambda_A,\lambda_B, \lambda_C} = H_{\lambda_B,\lambda_C}^{A \rightarrow B C} D^{J_{A}*}_{\lambda_A,\lambda_B - \lambda_C}(\phi, \theta, 0).

The LS coupling formula is used

.. math::
    H_{\lambda_{B},\lambda_{C}}^{A \rightarrow B+C} =
    \sum_{ls} g_{ls} \sqrt{\frac{2l+1}{2 J_{A}+1}} \langle l 0; s \delta|J_{A} \delta\rangle \langle J_{B} \lambda_{B} ;J_{C} -\lambda_{C} | s \delta \rangle q^{l} B_{l}'(q, q_0, d)

:math:`g_{ls}` are the fit parameters, the first one is fixed.  :math:`q` and :math:`q_0` is the momentum in rest frame for invariant mass and resonance mass.

:math:`B_{l}'(q, q0, d)`  (`~tf_pwa.breit_wigner.Bprime`) is Blatt-Weisskopf barrier factors. :math:`d` is :math:`3.0 \mathrm{GeV}^{-1}` by default.


Resonances model use Relativistic Breit-Wigner function

.. math::
   R(m) = \frac{1}{m_0^2 - m^2 -  i m_0 \Gamma(m)}

with running width

.. math::
   \Gamma(m) = \Gamma_0 \left(\frac{q}{q_0}\right)^{2L+1}\frac{m_0}{m} B_{L}'^2(q,q_0,d).

By using the combination rules, the amplitude is built automatically.


Helicity Angles
---------------

The helicity angle in TFPWA is defined as the roation between two coordinates systems.

The first one is :math:`(\vec{x}_0, \vec{y}_0, \vec{z}_0)`, the last one is :math:`(\vec{x}_1, \vec{y}_1, \vec{z}_1)`. We can calculate the Eular Angle between the two system. The rotation order is:

* 1. Rotate :math:`\alpha` around :math:`\vec{z}_0`. The :math:`\vec{y}_0` is rotated to :math:`\vec{y}_R`.
* 2. Rotate :math:`\beta` around :math:`\vec{y}_R`. The :math:`\vec{z}_0` is rotated to :math:`\vec{z}_1`.
* 3. Rotate :math:`\gamma` around :math:`\vec{z}_1`. The :math:`\vec{y}_R` is rotated to :math:`\vec{y}_1`.

From the rotation order, we can define that :math:`\vec{y}_R = \frac{\vec{z}_0 \times \vec{z}_1}{|\vec{z}_0 \times \vec{z}_1|}`, and then :math:`\beta` is in the range :math:`[0,\pi]`. The :math:`\alpha,\gamma` can be calculated in the range :math:`[-\pi,\pi]`, through :math:`\cos\alpha = \vec{y}_0 \cdot \vec{y}_R, \sin\alpha = - \vec{x}_0 \cdot \vec{y}_R` and :math:`\cos\gamma = \vec{y}_R \cdot \vec{y}_1, \sin\gamma = \vec{x}_1 \cdot \vec{y}_R`.

For the decay process, we can set a initial coordinate system. For example, we can choose :math:`\vec{x}_0=(1,0,0),\vec{z}_0=(0,0,1)` or the direction of total momentum.
And then we can define the new coordinate system after the first decay :code:`A -> R B` as :math:`\vec{z}_1 = \vec{p_{R}}` in the rest frame of :code:`A`. The :math:`\gamma` angle can set to 0, then :math:`\vec{y}_1 = \vec{y}_R`. Then the coordinate system is defined. Based on the two coordinate system, we can calculate the helicity angle as :math:`\phi=\alpha,\theta=\beta`.

To calculate helicity angle of the second decay :code:`R -> C D`, the first coordinate system has been defined as above. We need to keep the same coordinate system. And we define the second coordinate system by :math:`\vec{z}_1 = \vec{p_{C}}` and :math:`\gamma=0`, and calculate the helicity angle. The :math:`p_{C}` should boost to rest frame of :code:`R` after we boost to the rest frame of :code:`A`. The boost sequence will introduce a additional rotation of the coordinate system.

Due to the boost sequence of final particles, the coordinate system of each final particles in different decay chains is different. We need to do alignment for different decay chains before sum the amplitude over. We can record the roation and boost sequence, and combine then into a single object of Lorentz group, :math:`L_1 = \overleftarrow{R_y(\theta_2)R_z(\phi_2)B_z(\omega_2)R_y(\theta_1)R_z(\phi_1)B_z(\omega_1)}`, :math:`L_2 = \overleftarrow{R_y(\theta_2')R_z(\phi_2')B_z(\omega_2')R_y(\theta_1')R_z(\phi_1')B_z(\omega_1)}`, where :math:`\omega=\tanh^{-1}\frac{|p|}{E}`. The direction of the arrow is order of the operator. And then we can find the standalone rotation between the two coordinate system by solve :math:`\alpha,\beta,\gamma` from :math:`L_1 = \overleftarrow{[R_z(\gamma)R_y(\beta)R_z(\alpha)B_z(\omega)] L_2} = \overleftarrow{[L_1 L_2^{-1}] L_2}`. The two coordinate system both have :math:`\vec{z}=\vec{p}`, so only :math:`B_z(\omega)` remain. See `Chin.Phys.C 45 (2021) 6, 063103 <https://inspirehep.net/literature/1835597>`_ and `JHEP 12 (2022) 033 <https://inspirehep.net/literature/2153556>`_ for more information.

The two dimisional presentation of Lorentz group is used.

.. math::
   R_z(\phi) = \begin{pmatrix}
   e^{-i\frac{\phi}{2}} & 0 \\
   0 & e^{-i\frac{\phi}{2}}
   \end{pmatrix},
   R_y(\theta) = \begin{pmatrix}
   \cos\frac{\theta}{2} & -\sin\frac{\theta}{2} \\
   \sin\frac{\theta}{2} & \cos\frac{\theta}{2}
   \end{pmatrix},
   B_z(\omega) = \begin{pmatrix}
   e^{-\frac{\omega}{2}} & 0 \\
   0 & e^{\frac{\omega}{2}}
   \end{pmatrix}.

Then the angle can be solved as

.. math::
   \alpha  + \gamma = 2\arg L_{22},
   \alpha  - \gamma = - 2\arg L_{21},
   \cos\beta = L_{11} L_{22} + L_{12} L_{21}

The range of :math:`\beta` is :math:`[0,\pi]` and the range of :math:`\alpha,\gamma` are :math:`[-2\pi,2\pi]`. The :math:`4\pi` range is required for fermion, whose :math:`2\pi` rotation will contribute a negative sign. It also raise a problem for the defination rotation to opposite direction. In the first decay :code:`A -> R B`, we define the new coordinate as :math:`\vec{z}_1 = \vec{p_{R}}`, but the :math:`\vec{p_{B}}` is the opposite direction. Additional rotation from :math:`\vec{p_{R}}` to the opposite :math:`\vec{p_{B}}` is required, which will affect the phase of fit parameters. In TFPWA, such rotation is defined as :math:`R_x(\pi)=[\overleftarrow{R_y(\pi-\theta)R_z(\phi-\pi)}][\overleftarrow{R_y(\theta)R_z(\phi)}]^{-1}=\overleftarrow{R_y(\pi)R_z(-\pi)}`.  :math:`\phi-\pi` and :math:`\pi-\theta` are the angles if you calculate from :math:`\vec{z}_1 = \vec{p_{B}}`, but we fix the phase difference to :math:`-\pi`. If we calculate directly from :math:`\vec{z}_1 = \vec{p_{B}}`, the phase difference would be random sign :math:`\pm\pi`, which would cancel some interferences that should exist.
